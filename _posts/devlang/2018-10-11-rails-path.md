---
layout:     post
title:      "Rails 目录结构"
date:       2018-10-11
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - rails
---

# Rails 目录结构 #

## 目录 ##

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Rails 目录结构](#rails-目录结构)
    - [目录](#目录)
    - [Rails 项目的目录结构](#rails-项目的目录结构)
        - [app/](#app)
            - [app/controllers](#appcontrollers)
            - [app/models](#appmodels)
            - [app/views](#appviews)
            - [app/helpers](#apphelpers)
            - [app/assets](#appassets)
        - [config/](#config)
        - [db/](#db)
        - [lib/](#lib)
            - [lib/tasks](#libtasks)
        - [log/](#log)
        - [public/](#public)
        - [bin/](#bin)
        - [test/](#test)
        - [tmp/](#tmp)
            - [vendor/assets](#vendorassets)
        - [其他根目录下的档案](#其他根目录下的档案)
    - [References](#references)

<!-- markdown-toc end -->

## Rails 项目的目录结构 ##

### app/ ###

app 目录是你主要工作的地方，不同子目录存放了 Models、Controllers、Views、Helpers 和 Assets 等档案。

#### app/controllers ####

Controller 的类别档案存放在这里

#### app/models ####

Model 的类别档案存放在这里

#### app/views ####

View 的样本(template)档案，依照不同 Controllers 分子目录存放。

#### app/helpers ####

Helper 一些在 Views 中可以使用的小方法，用来产生较复杂的 HTML。默认的 Helper 档案命名是对应 Controller 的，不过并不强制，定义在任一个 Helper 档案中的方法，都可以在任何 Views 中使用。

#### app/assets ####

Assets 静态档案存放在这里，包括有 JavaScript、Stylesheets 样式表和 Images 图档。详细的用法会在 Assets 一章中介绍。

### config/ ###

虽然 Rails 的原则是惯例优于设定，不过还是有一些需要设定的地方。这个目录下存放了例如数据库设定档 database.yml、路由设定 routes.rb、应用程式设定档 application.rb 和不同执行环境的设定档在 config/environments 目录下。

### db/ ###

数据库 Schema(纲要) 和定义档 migrations

### lib/ ###

如果你有一些共享的类别或模块档案，可以放在这里，然后用 require 加载。例如一个放在 lib/foobar.rb 的类别或模组档案，可以在要使用的 .rb 档案中这样加载：

``` rails
require "foobar"
```

如果放在子目录 lib/foo/bar.rb 的话：

``` rails
require "foo/ba
```

#### lib/tasks ####

Rake 任务档案存放在这里，我们会在 Rails 锦囊妙计 一章介绍 Rake。

### log/ ###

不同执行环境的 log 档案会分别记录在这里

### public/ ###

这个目录对 Web 服务器来说，就是文件根目录(document root)，也就是唯一可以在网络上读取到的目录。

### bin/ ###

Rails 的脚本档案，例如执行 bin/rake。

### test/ ###

单元测试、功能测试及整合测试的档案。本书会改用 RSpec 做测试，所以这一个目录会被砍掉。RSpec 的测试档案会放在 spec/目录下。

### tmp/ ###

. 用来存放暂时用途的档案

#### vendor/assets ####

可将第三方的 CSS/JavaScript 函式库(没有提供 Gem 安装版本的)复制一份放在这里。

### 其他根目录下的档案 ###

- config.ru 用来启动应用程式的 Rack 设定档
- Gemfile 设定你的 Rails 应用程式会使用哪些 Gems
- README.md 你的应用程式使用手册。你可以用来告诉其他人你的应用程式是做什么用的，如何使用等等。这会是 Github 上的专案首页。
- Rakefile 用来加载可以被命令列执行的 Rake 任务

> [返回目录](#目录)

## References

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

> [返回目录](#目录)