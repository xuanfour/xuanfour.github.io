---
layout:     post
title:      "Ruby on Rails Tips"
date:       2018-10-11
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - ruby
    - rails
---

# Ruby on Rails Tips #

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Ruby on Rails Tips](#ruby-on-rails-tips)
    - [目录](#目录)
    - [logger](#logger)
        - [层级](#层级)
    - [Puma 服务器支持 SSL](#puma-服务器支持-ssl)
    - [require 引用文件路径方法与问题总结](#require-引用文件路径方法与问题总结)
        - [引用一个文件](#引用一个文件)
        - [引用一个目录下所有文件](#引用一个目录下所有文件)
    - [format.json](#formatjson)
    - [RESTful API 配置 CORS 实现跨域请求](#restful-api-配置-cors-实现跨域请求)
    - [其他](#其他)
    - [References](#references)

<!-- markdown-toc end -->

## logger ##

### 层级 ###

- debug
- info
- warn
- error
- fatal

## Puma 服务器支持 SSL ##

``` bash
puma -b 'ssl://0.0.0.0:3000?key=/home/xuanfour/.ssh/XXX.key&cert=/home/xuanfour/.ssh/XXX.pem'
```

## require 引用文件路径方法与问题总结 ##

同一目录下的文件，如/usr/local/ruby/foo.rb 与/usr/local/ruby/bar.rb 两个文件。
如果直接在 foo.rb 中 `require 'bar'` 执行时会报找不到 bar.rb 错误。
这是因为运行 ruby /usr/local/ruby/foo.rb 时会在 ruby 安装的 lib 目录和/home/oldsong/目录下查找 bar.rb。而不会去 rb 文件的目录 /usr/local/ruby/ 下查找。所以除引用系统 rb 外，require 中不能用相对路径。

下面介绍几种引用单个和目录下所有 rb 的方法。

### 引用一个文件 ###

例: 引用当前 rb 同目录下的 file_to_require.rb

- require File.join(__FILE_, '../file_to_require')。
- require File.expand_path('../file_to_require', __FILE__)
- require File.dirname(__FILE__) + '/file_to_require'

其中，File.expand_path 是 Rails 常用的做法。
__FILE__为常量，表示当前文件的绝对路径，如/home/oldsong/test.rb

``` rails
$LOAD_PATH.unshift(File.dirname(__FILE__))
require 'bar'
```

先把目录加入 LOAD_PATH 变量中，然后可直接引用文件名。

### 引用一个目录下所有文件 ###

Ruby 没有 Java 中的 import java.io.*;
引用时不能用通配符，估计以后的版本有可能加上。

例：引用当前 rb 相同目录下 lib/文件下所有*.rb 文件。

``` rails
Dir[File.dirname(__FILE__) + '/lib/*.rb'].each {|file| require file }
```

使用 gem 搞定

https://rubygems.org/gems/require_all

> [返回目录](#目录)

## format.json ##

首先在 controller#action 中添加对 json 的响应。

``` rails
def index
  @posts = Post.all
  respond_to do |format|
    format.html
    format.json
  end
end
```

format.json 会自动寻找 index.json 文件，我们可以用 jbuilder 写，创建 index.json.jbuilder

``` rails
json.array! @posts do |post|
  json.extract! post, :topic, :contact_person, :created_at
end
```

这样就会返回如下结构的 json

``` json
[{topic: xxx, contact_person: xxx, created_at: xxx},
 {...},
 {...}]
```

> [返回目录](#目录)

## RESTful API 配置 CORS 实现跨域请求 ##

Rails 框架为例。注意：这只是一个很简单的例子，为了展示其原理，建议只在安全要求不高的项目上使用这种方法。Rails 有专门的 [Rack CORS 中间件](https://github.com/cyu/rack-cors) 可以处理这个问题。

在一个 Controller 或者 application_controller.rb 中添加 before_filter 和 after_filter。前者用来回应浏览器的“事前检查”，如果浏览器发来了 OPTIONS 请求，则返回一些响应头，并结束处理；后者则用来给响应添加 CORS 的响应头：

``` rails

# file: some_controller.rb

before_filter :cors_preflight_check
after_filter :cors_set_headers

# ...

def cors_preflight_check
  if request.method == 'OPTIONS'
    headers['Access-Controll-Allow-Origin'] = '*'
    headers['Access-Controll-Allow-Methods'] = 'POST, GET, OPTIONS'
    headers['Access-Controll-Allow-Headers'] = 'X-Requested-With, Content-Type, Accept'
    headers['Access-Controll-Max-Age'] = '1728000'
    render :text => '', :content-type => 'text/plain'
  end
end

def cors_set_headers
  headers['Access-Controll-Allow-Origin'] = '*'
  headers['Access-Controll-Allow-Methods'] = 'POST, GET, OPTIONS'
  headers['Access-Controll-Max-Age'] = '1728000'
end
```

最后，别忘了在 routes.rb 中允许 OPTIONS 请求：

``` rails
match 'controller', to: 'controller#action', via: [:options] ＃ 添加此行
```

## 其他 ##

- 左值不能省略 self

> [返回目录](#目录)

## References ##

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

> [返回目录](#目录)
