---
layout:     post
title:      "Rails 样例"
date:       2018-10-11
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - rails
---

# Rails 样例

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Rails 样例](#rails-样例)
    - [目录](#目录)
    - [新建项目](#新建项目)
    - [设置时区](#设置时区)
    - [测试报告](#测试报告)
    - [References](#references)

<!-- markdown-toc end -->


## 新建项目 ##

``` bash

# 创建新的项目
rails new sample_app
cd sample_app

# 编辑 Gemfile
vim Gemfile

# 安装 gem
bundle install --without production
bundle update

# 编辑说明文件
vim README.md

# 初始化 Git 仓库
# git init
git add -A
git commit -m 'init'

# 启动服务，使用 C-c 中断服务
bin/rails server

# 如果有远程仓库
git remote add origin git@<url>:<user>/<repo>.git
# 如果首次推送使用
git push -u origin --all
# 如果再次推送使用
git push

# 有大的变更前最好新建一个分支
git checkout -b <branch-name>
# 首次推送分支到远程仓库
git push -u origin <branch-name>
# 修改完成后提交并合并到主分支
git add -A
git commit -m 'finish xxx'
git checkout master
git merge <branch-name>

# 生成控制器，命令的控制器名使用驼峰式，创建的控制器文件名是蛇底式
bin/rails generate controller <ControllerName> <action_name>
# 撤销前一个命令
bin/rails destroy controller <ControllerName> <action_name>

# 生成模型
bin/rails generate model <ModelName> <attr_name>:<type>
# 撤销前一个命令
bin/rails destroy model <ModelName>

# 生成数据迁移
bin/rails db:migrate
# 撤销前一个命令
bin/rails db:rollback
# 回到最开始的状态，下面的 `0` 可以修改为其他数字以回到相应版本
bin/rails db:migrate VERSION=0

# 修改 `config/routes.rb` 增加控制器动作的路由
# 将发给 `<controller>/action` 的请求映射到控制器动作。另外，get 表达这个路由响应的是 Get 请求。
get `<controller>/action`

# 集成测试
bin/rails generate integration_test site_layout

# 生成测试数据，编辑文件 `test/fixtures/xxxx.yml`
# `gem faker` 可以用半真实的名字和电子邮件地址创建示例用户
# 向数据库中添加示例用户的 ruby 代码，编辑文件 `db/seeds.rb`
User.create!(name: 'Example User',
             email: 'example@railstutorial.org',
             password: 'foobar',
             password_confirmation: 'foobar')

99.times do |n|
  name = Faker::Name.name
  email = "example-#{n+1}@railstutorial.org"
  password = 'password'
  User.create!(name: name,
               email: email,
               password: password,
               password_confirmation: password)
end

# 还原数据库
bin/rails db:migrate:reset
# 生成示例数据
bin/rails db:seed
```

## 设置时区 ##


``` rails
# file: config/application.rb
# 国际化本地设置
config.i18n.default_locale = 'zh-CN'
# 显示为北京时间
config.time_zone = "Beijing"
# 存入数据库本地时区时间
config.active_record.default_timezone = :local
# optional: 关闭以 UTC 格式存入数据库并读取以本地时区格式读取的功能
# config.active_record.time_zone_aware_attributes = false
```

## 测试报告 ##


``` rails
# file: Gemfile -> test group
gem 'minitest',                 '5.10.3'
gem 'minitest-reporters',       '1.1.14'

# file: test/test_helper.rb
require 'minitest/reporters'
Minitest::Reporters.use!
```

> [返回目录](#目录)

## References

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

> [返回目录](#目录)
