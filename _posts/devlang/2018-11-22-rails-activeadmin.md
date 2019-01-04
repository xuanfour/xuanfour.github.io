---
layout:     post
title:      "Rails ActiveAdmin 学习"
date:       2018-10-19
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - rails
    - activeadmin
    - gem
---

# Rails ActiveAdmin 学习 #

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Rails ActiveAdmin 学习](#rails-activeadmin-学习)
    - [目录](#目录)
    - [安装](#安装)
        - [基础](#基础)
        - [生成 activeadmin 框架](#生成-activeadmin-框架)
        - [配置 rolify](#配置-rolify)
        - [本地化](#本地化)
        - [配置 cancan](#配置-cancan)
        - [为 activeadmin 配置 cancan 权限](#为-activeadmin-配置-cancan-权限)
        - [启动服务](#启动服务)
        - [如果要关闭用户登录验证功能，可以用：](#如果要关闭用户登录验证功能可以用：)
        - [Comment](#comment)
    - [Utility Navigation（导航）](#utility-navigation 导航)
    - [创建 Resources](#创建-resources)
        - [permit_params](#permitparams)
        - [定义一个 Resource 中的 action](#定义一个-resource-中的-action)
    - [自定义 Menu](#自定义-menu)
        - [添加自定义的 menu](#添加自定义的-menu)
        - [自定义 resource 的 index 页面](#自定义-resource-的-index-页面)
    - [自定义 Actions](#自定义-actions)
    - [Form(model 的创建或者修改表单)](#formmodel-的创建或者修改表单)
    - [增加 action 的按钮](#增加-action-的按钮)
    - [项目汉化](#项目汉化)
        - [ActiveAdmin 汉化](#activeadmin-汉化)
            - [第一步：局部汉化](#第一步：局部汉化)
            - [第二步：框架汉化](#第二步：框架汉化)
            - [第三步：修改配置](#第三步：修改配置)
        - [Model 国际化](#model-国际化)
        - [Device 国际化](#device-国际化)
            - [错误列表](#错误列表)
    - [ActiveAdmin 更新](#activeadmin-更新)
    - [相关资源](#相关资源)
    - [References](#references)

<!-- markdown-toc end -->

## 安装 ##

### 基础 ###

``` shell
rails new auth
```

添加下面的 Gem 到 Gemfile

- activeadmin 后台管理
- devise：负责用户注册、登录、退出、找回密码等操作。
- cancancan：负责角色建立、对角色授权、在页面中根据授权是否显示元素，以及模型中超出授权时抛出异常。
- rolify：负责将用户与角色关联。
- draper：model 装饰，添加一个面向对象的表示逻辑层，增强性 helper。
- pundit：针对用户和类的权限管理。

``` ruby
gem 'activeadmin'
gem 'devise'
gem 'cancancan'
gem 'rolify'
# gem 'draper'
# gem 'pundit'
```

``` shell
bundle install
```

### 生成 activeadmin 框架 ###

其中包含了 devise

``` shell
rails g active_admin:install User
rake db:migrate
rake db:seed (添加一个用户 admin@example.com:password)
```

### 配置 rolify ###

``` shell
rails g rolify Role User
rake db:migrate
```

为第一个用户添加角色, 运行 rails console

``` ruby
User.first.add_role :admin
User.first.has_role? :admin
```

如果第二行返回为 true， 则表示角色设置成功了。另外需要再添加一个普通用户作为测试，同样在 rails console 环境下处理

``` ruby
User.create!(email: 'general@example.com', password: 'password', password_confirmation: 'password')
```

### 本地化 ###


``` ruby
# config/application.rb
config.i18n.load_path += Dir[Rails.root.join('config', 'locales', '**',
        '*.{rb,yml}').to_s]
config.i18n.default_locale = :"zh-CN"
```

按照 rails 风格，config/locales 就是放置语言包的地方，不建议更改。然后我们就可以利用这样的风格来管理语言包了。

``` text
+locales--
 |+zh-CN
  |default.yml
  |devise.yml
  |..
 |+en
  |default.yml
  |devise.yml
  |..
```

### 配置 cancan ###

``` shell
rails g cancan:ability
```

配置 admin 可以干所有的事情，一般用户只能读取数据

``` ruby
# app/models/ability.rb
if user.has_role? :admin
  can :manage, :all
else
  can :read, :all
end
```

### 为 activeadmin 配置 cancan 权限 ###

这个应该是最重要的部分

``` ruby
# config/initialize/active_admin.rb
config.authorization_adapter = ActiveAdmin::CanCanAdapter
config.cancan_ability_class = "Ability"
config.on_unauthorized_access = :access_denied
```

配置完上面的内容以后

``` ruby
# app/controller/application_controller.rb
def access_denied(exception)
  redirect_to(users_path, alert: exception.message)
end
```

``` ruby
# config/routes.rb
root to: 'admin/dashboard#index'
```

### 配置邮件服务器 ###

在开发环境下，需要配置下列内容：

``` ruby
# config/environments/development.rb:
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

### 配置信息提示页面 ###

``` ruby
# app/views/layouts/application.html.erb

<p class="notice"><%= notice %></p>
<p class="alert"><%= alert %></p>
```

### 启动服务 ###

``` shell
rails s
```

访问 http://localhost:3000/admin , 分别利用不同的用户登陆，进入 User 菜单，可以看到对 admin 和非 admin 用户所呈现的菜单是不一样的。一般用户只能读取，而 admin 用户可以修改，增加，删除。由此，activeadmin 对权限的支持也异常漂亮。

> [返回目录](#目录)


### 如果要关闭用户登录验证功能，可以用： ###

``` shell
# initializer/active_admin
config.current_user_method = false
config.authentication_method = false
```

### Comment ###

因为不需要 comment(注解)这个功能，所以在 initializer 中的 active_admin 中关闭这个功能

``` ruby
# For the entire application:
ActiveAdmin.setup do |config|
  config.comments = false
end

# For a namespace:
ActiveAdmin.setup do |config|
  config.namespace :admin do |admin|
    admin.comments = false
  end
end

# For a given resource:
ActiveAdmin.register Post do
  config.comments = false
end
```

## Utility Navigation（导航） ##

在右上角有一些快速导航按钮，默认的有两个，一个是当前的 admin 用户，另外一个是登出按钮，我们可以增加导航按钮

``` ruby
ActiveAdmin.setup do |config|
  config.namespace :admin do |admin|
    admin.build_menu :utility_navigation do |menu|
      menu.add label: "ActiveAdmin.info", url: "http://www.activeadmin.info",
                                          html_options: { target: :blank }
      admin.add_current_user_to_menu  menu
      admin.add_logout_button_to_menu menu
    end
  end
end
```

## 创建 Resources ##

添加一个 model，然后把 model 加入 active admin resources


``` shell
bin/rails generate model Post name:string title:string content:text
# => app/model/post.rb
bin/rails generate active_admin:resource Post
# => app/admin/posts.rb
```

执行后会生成 app/admin/post.rb 文件

### permit_params ###

使用 permit_params 方法来定义哪些属性可以被修改,如果修改了没有被 permit_params 定义的属性，修改不会生效

``` ruby
ActiveAdmin.register Post do
  permit_params :title, :content, :publisher_id
end
```

### 定义一个 Resource 中的 action ###

默认的，所有的 CRUD 的 actions 都可以操作，如果要禁用其中的某些操作，用如下定义：

``` ruby
ActiveAdmin.register Post do
  actions :all, except: [:update, :destroy]
end
```

## 自定义 Menu ##

一个 resource 默认都会在全局导航栏上，如果要禁止一个 resource 出现在全局导航栏上，我们可以用：

```
ActiveAdmin.register Post do
  # menu false
  # menu label: "自定义标题",priority: 1
end
```

menu 有 4 个选项可以用：

- :label    - 指定该 menu 的名称
- :parent   - 指定一个顶级菜单
- :if       - 指定一个条件
- :priority - 默认为 10，在全局导航栏上的位置

### 添加自定义的 menu ###

``` ruby
# config/initializers/active_admin.rb

config.namespace :admin do |admin|
  admin.build_menu do |menu|
    menu.add label: "The Application", url: "/", priority: 0

    menu.add label: "Sites" do |sites|
      sites.add label: "Google",
                url: "http://google.com",
                html_options: { target: :blank }
      sites.add label: "Github",
                url: "http://github.com"
    end
  end
end
```

### 自定义 resource 的 index 页面 ###

提供 4 中样式，Block，Blog，Grid，Table，一般我们用的是 table，也是默认的样式。这里只介绍 table。
默认的，index 页面会展示对应的 model 的所以字段，可供查看，修改，删除。
如果要自定义字段，可以用：

``` ruby
index do
  selectable_column
  column :title
  column "My custom name", :name
end
```

这些自定的字段要被 index 包裹：

- selectable_column 显示勾选框，用于批量操作
- column 显示什么字段，该字段必须是 model 的字段名，可以给这个字段另取一个别名

还可以根据条件设置特别的 row 样式，这个 some_style 样式放在 app/asset/stylesheets/active_admin.scss 中

``` ruby
index(row_class: ->item { 'some_style' if item.is_show }) do
end
```

## 自定义 Actions ##

如果要给 resource 设置链接到查看，修改，删除这几个按钮，可以用 actions 方法

``` ruby
index do
  selectable_column
  column :title
  actions
end
```

也可以增加自定的链接

``` ruby
index do
  selectable_column
  column :title
  actions do |post|
    item "Preview", admin_preview_post_path(post), class: "member_link"
  end
end
```

获取重新设置链接

``` ruby
index do
  column :title
  actions defaults: false do |post|
    item "View", admin_post_path(post)
  end
end
```

## Form(model 的创建或者修改表单) ##

默认的表单是展示所有的字段

``` ruby
form do |f|
  f.semantic_errors # shows errors on :base
  f.inputs          # builds an input field for every attribute
  f.actions         # adds the 'Submit' and 'Cancel' buttons
end
```

示例：

``` ruby
form title: 'A custom title' do |f|
    inputs 'Details' do
      input :part1
      input :part2, label: "Publish Post At"
      li "Created at #{f.object.created_at}" unless f.object.new_record?
      input :part3
    end
    panel 'Markup' do
      "The following can be used in the content below..."
    end
    inputs 'Content', :part3
    para "Press cancel to return to the list without saving."
    input :created_at, as: :datepicker,
            datepicker_options: {
                min_date: "2013-10-8",
                max_date: "+3D"
            }
    actions
  end
```

## 增加 action 的按钮 ##

link_to path 中的 path 指定的方式是

1. 命名空间_model 的复数形式_path
2. controller 名称_方法名_path

``` ruby
action_item only: :index do
  link_to '刷新疑似状态', admin_app_oral_memories_path, notice: "刷新成功"
end
```

增加 batch 操作按钮

``` ruby
batch_action "封禁" do |selection|
end
```

Index Filter 过滤器

``` ruby
filter :name, label: "name"
```

一般的，通过上面这个形式就好了，activeadmin 会自动判断其类型。

或者有另个情况，有个关联表。

``` ruby
filter :location_id, label: "地点", as: :select, collection: AppExamLocation.all.map{|x| [x.location,x.id]}
```

通过:as 可以指定类型，提供这一下这几种类型


``` ruby
:string - A drop down for selecting “Contains”, “Equals”, “Starts with”, “Ends with” and an input for a value.
:date_range - A start and end date field with calendar inputs
:numeric - A drop down for selecting “Equal To”, “Greater Than” or “Less Than” and an input for a value.
:select - A drop down which filters based on a selected item in a collection or all.
:check_boxes - A list of check boxes users can turn on and off to filter
```

> [返回目录](#目录)

## 项目汉化 ##

### ActiveAdmin 汉化 ###

#### 第一步：局部汉化 ####

``` ruby
ActiveAdmin.register AdminUser do
  menu :label => "用户管理"

  index do
    column "邮箱",:email
    column "最近登录",:current_sign_in_at
    column "上次登录",:last_sign_in_at
    column "登录次数",:sign_in_count
    default_actions
  end

  filter :email, :label=>"邮箱"

  form do |f|
    f.inputs "用户资料" do
      f.input :email ,:label=>"邮箱"
      f.input :password ,:label=>"密码"
      f.input :password_confirmation ,:label=>"重复密码"
    end
    f.actions
  end

  # 右侧帮助
  sidebar :help,:only => :index do
    "如果您在使用后台管理时遇到问题，请联系 robot.zhu@icitymobile.com"
  end
end
```

按上述设置后，页面部分内容将变成中文。

- menu 菜单栏文字
- index column 列表中某列
- filter label 筛选器标签
- form inputs 表单的标题
- form input label 单个文本输入框前的标签

这个时候看，整个框架还是英文的。

#### 第二步：框架汉化 ####

导入 ActiveAdmin 提供的语言文件。根据需要选择。简体中文就选择 zh-CN.yml。

- 地址：https://github.com/activeadmin/activeadmin/tree/master/config/locales
- 中文：https://github.com/activeadmin/activeadmin/blob/master/config/locales/zh-CN.yml

将 zh-CN.yml 复制到自己的 config/locales/目录下。

#### 第三步：修改配置 ####

修改 config/application.rb 文件，添加下面两行。

``` ruby
config.i18n.available_locales = [:"zh-CN", :en]
config.i18n.default_locale = :"zh-CN"
```

重启 Rails Server。

整个框架就变成中文了。

### Model 国际化 ###

实际上面这么做之后，还有少量地方仍然是英文。
比如：导航栏上的模块名称（Posts），右侧的“新建 Post”按钮。

我们肯定希望“Posts”显示为“博文”，“新建 Post”显示为“新建博文”。

这个时候需要在语言文件 zh-CN.yml 里加上 models 的国际化。

``` yaml
activerecord:
  models:
    user: '用户'
    post: '博文'
    organization: '机构'
```

### Device 国际化 ###

下载汉化包 devise.zh-CN.yml，并复制到自己的 config/locales/目录下。
下载地址：https://github.com/plataformatec/devise/wiki/I18n

#### 错误列表 ####

错误信息：

``` ruby
ActionView::Template::Error (translation missing: zh-CN.time.formats.long):
    1: insert_tag renderer_for(:index)
  app/admin/admin_user.rb:6:in `block (2 levels) in <top (required)>'
```

解决办法

引入 Rails 的语言文件。复制内容至 zh-CN.yml 文件中。

- 地址：https://github.com/tsechingho/rails-i18n/tree/master/rails/locale
- 中文：https://github.com/tsechingho/rails-i18n/blob/master/rails/locale/zh-CN.yml

> [返回目录](#目录)

## ActiveAdmin 更新 ##

你可以键入如下命令进行对它的升级

``` shell
rails generate active_admin:assets
```

如果提示：uninitialized constant Admin::DashboardController
这个时候，需要 dashboard view（app/admin/dashboards.rb）和初始化的时候一样。

## Rails Activeadmin 界面构成方法解析 ##

以一个 PMS 系统中的供应商界面的功能来做例子，并没有将界面与后台代码解偶，而是绑定在了一起。controller 是这个文件，view 也是这个界面，只有 model 是另外的文件，这是 rails 的要求。该界面数据和数据库的一张表，或者说一个 model 相对应。一个界面就和一张数据表绑定，非绑定数据界面另放 view 中 render。理解这一点才能更好的理解功能的实现。

``` ruby
#supplier.rb 文件：
ActiveAdmin.register Supplier do

#permit_params:允许数据库传到界面的参数
  permit_params :supplier_code, :supplier_type, :supplier_name, :supplier_simple, :company_address, :company_tel, :company_fax, :supplier_status, :company_account,
                :account_name, :company_tax, :supplier_order, :contact_count, :attachment_count, :material_count, :remark, :operator_id, :payment_term
#分页开启，和每页数据量
  config.paginate = true
  config.per_page = 20
  #默认排序
  config.sort_order = 'supplier_order'

  #禁用功能
  config.filters = false
  config.batch_actions = false

#绑定的数据表的信息展示,将展示的信息做处理，如果不写这段，数据表中的数据仍然会显示，　但是会显示所有字段，并且显示的列名为数据表的字段名，从网页显示的角度来说并不美观
index :title => '供应商列表' do
    selectable_column
    #id_column
    column "编码", :supplier_code
    column "类别", :supplier_type_name
    column "名称", :supplier_name
    column "公司地址", :company_address
    column "状态", :supplier_status_name
    column "备注", :remark
    column "属性" do |f|

      if f.attachment_count > 0
        span  do
          image_tag "/assets/icons/address.png", height: '20', width: '20', title: "有附件"
        end
      end
    end
    actions
  end

#界面方法，如非绑定数据界面的后台方法的
 collection_action :get_users, :method => :post do
    supplier_id = params[:id]
    render json: SupplierContact.format_contact_data(supplier_id)
  end

  collection_action :save_contact, :method => :post do
    render json: SupplierContact.save_contact_data(params)
  end

＃form 表单显示　和 index 一样是一种数据展示的方式，其他的还有 grid,Table,blog,Blocks
＃
form do |f|
    f.inputs "供应商信息" do

      #只有新建时才更新
      if resource.supplier_code.present?
        supplier_code = resource.supplier_code
      else
        supplier_code = Base.get_model_code('GYS', 4, 'supplier')
      end

      f.input :supplier_code, :hint => "供应商唯一编号", :input_html => { :value => supplier_code, :readonly => true}, :label=> "供应商编号"

      f.input :supplier_name, :label=> "供应商全称", :required => true
      f.input :supplier_simple, :label=> "简称"
      f.input :supplier_type, :as => :select, :collection =>  resource.supplier_type_ary, :include_blank => false, :label=> "供应商类别"
      f.input :supplier_status, :as => :select, :collection =>  resource.supplier_status_ary, :include_blank => false, :label=> "供应商状态"
      f.input :company_address, :label=> "公司地址"
      f.input :company_tel, :label=> "公司座机"
      f.input :company_fax, :label=> "公司传真"
      f.input :company_account, :label=> "公司账户"
      f.input :account_name, :label=> "账户名称"
      f.input :company_tax, :label=> "税号"
      f.input :payment_term, :label=> "付款周期"
      f.input :remark, :input_html => { :rows => "5"}, :label=> "备注"
      f.input :operator_id, :as => :hidden, :input_html => {:value => current_active_admin_user.id}
    end
    f.actions
  end


 end
```

## 增加全局错误信息提示 ##

### 定义错误 ###

``` ruby
class User < ActiveRecord::Base
  before_destroy :before_destroy_check

  def before_destroy_check
    errors.add(:base, '不能删除管理员') if id < 2
    throw :abort if errors.anyblank?
  end
end
```

### 显示错误 ###

``` ruby
form do |f|
  f.semantic_errors *f.object.errors.keys
  # ...
end
```

或者直接打补丁

``` ruby
config/initializers/active_admin_patches.rb.

class ActiveAdmin::ResourceController
  def check_model_errors(object)
      return unless object.errors.any?
      flash[:error] ||= []
      flash[:error].concat(object.errors.full_messages)
  end
end

class ActiveAdmin::ResourceDSL
  alias_method :old_run_registration_block, :run_registration_block
  def run_registration_block(&block)
    old_run_registration_block(&block)
    instance_exec { after_destroy :check_model_errors }
  end
```

## 相关资源 ##

- GitHub:   <https://github.com/activeadmin/activeadmin>
- 官方文档：<https://activeadmin.info/index.html>
- 示例网址：<https://demo.activeadmin.info>
- 邮箱列表：<https://groups.google.com/group/activeadmin>
- 其他相关：http://blog.csdn.net/feng88724/article/details/49124281

> [返回目录](#目录)

## References ##

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

- https://www.jianshu.com/p/0512a168733d
- https://blog.csdn.net/feng88724/article/details/49101487
- https://blog.csdn.net/life_is_crazy/article/details/72778227

> [返回目录](#目录)
