---
layout:     post
title:      "Ruby and Rails 常用方法函数"
date:       2018-10-11
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - ruby
    - rails
---

# Ruby and Rails 常用方法函数 #

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Ruby and Rails 常用方法函数](#ruby-and-rails-常用方法函数)
    - [目录](#目录)
    - [常用方法](#常用方法)
        - [`String.split`](#stringsplit)
        - [`Array.join`](#arrayjoin)
        - [`String.downcase`](#stringdowncase)
        - [`String.upcase`](#stringupcase)
        - [`String.reverse`](#stringreverse)
        - [`Array.shuffle`](#arrayshuffle)
        - [`Object.inspect`](#objectinspect)
        - [`Object.class`](#objectclass)
        - [`Class.superclass`](#classsuperclass)
        - [`Hash.merge(other_hash)`](#hashmergeotherhash)
        - [`singularize` 和 `pluralize`](#singularize-和-pluralize)
        - [`head`、`render` 和 `redirect_to`](#headrender-和-redirectto)
        - [`redirect_back`](#redirectback)
        - [HashWithIndifferentAccess](#hashwithindifferentaccess)
    - [References](#references)

<!-- markdown-toc end -->

## 常用方法

### `String.split`

字符串拆分成数组。

### `Array.join`

数组组合成字符串。

### `String.downcase`

返回小写字符串。

### `String.upcase`

返回大写字符串。

### `String.reverse`

反转字符串内容。

### `Array.shuffle`

返回乱序数组。

### `Object.inspect`

返回被调用对象的字符串字面量。

### `Object.class`

返回类。

### `Class.superclass`

返回类的父类。

### `Hash.merge(other_hash)`

返回一个新的散列，新散列是两个散列的合集，如果散列的键有重复，那么以 other_hash 的值为新散列的值。

### `singularize` 和 `pluralize`

- `singularize` 获得一个字符串的单数
- `pluralize` 获得一个字符串的复数

### `head`、`render` 和 `redirect_to`

从控制器的角度来看，创建 HTTP 响应有三种方法：

- 调用 `render` 方法，向浏览器发送一个完整的响应；
- 调用 `redirect_to` 方法，向浏览器发送一个 HTTP 重定向状态码；
- 调用 `head` 方法，向浏览器发送只含报头的响应；

从执行来看，有两种方式：

- `render` 是渲染，只是渲染了一个新的模版，没有执行相应的 action 方法。
- `redirect_to` 是跳转，实现 action 方法的跳转，向浏览器发起一个新的请求。

当 Rails 程序运行到 redirect_to 时，需要等待浏览器发送一个新的 http 请求再继续执行后面的代码。服务器发送 302 HTTP 状态码到浏览器并重定向，客户端(用户浏览器)将发送一个新的请求到服务器，action 将被执行。
运行 render 时不会执行指定 action 的代码，直接渲染页面。

控制器中的代码执行到 render 和 redirect_to 时，如果两者不是放在最后，并不会跳出并结束当前 action。

当涉及到表单提交时，数据库记录更新成功使用 redirect_to，更新失败使用 render 除了避免表单重复提交之外，如果表单提交失败，之前表单填写的信息还会存在，增强用户体验。

### `redirect_back`

`redirect_back(fallback_location: jump_path)`回到上一次访问的页面，如果 HTTP_REFERER 来源不存在，跳转到参数指定的位置。

> [返回目录](#目录)

### HashWithIndifferentAccess ###

Rails 的 ActiveSupport::HashWithIndifferentAccess 需求文件：

``` rails
require "active_support/core_ext/hash/indifferent_access"
```

ruby 2.0 引入了 keyword arguments，方法的参数可以这么声明

``` rails
def foo(bar: 'default')
  puts bar
end

foo # => 'default'
foo(bar: 'baz') # => 'baz'　　
```

在某些情况下，参数可能已经保存到了一个 hash 中的时候，也可以这么调用

``` rails
params = {bar: 'baz'}
foo(params) # => 'baz'
```

在 rails 中，请求传过来的参数都会变成 HashWithIndifferentAccess，可以通过 Symbol 或者 String 作为 key 获取 value

``` rails
params = {bar: 'baz'}.with_indifferent_access
params[:bar] # => 'baz'
params['bar'] # => 'baz'
```

如果直接将 HashWithIndifferentAccess 作为参数传给 keyword arguments 的方法，是行不通的

``` rails
params = {bar: 'baz'}.with_indifferent_access
foo(params) #  ArgumentError: wrong number of arguments (1 for 0)
```

这是因为 HashWithIndifferentAccess 中是以 String 作为 key 的，本质上和以下的错误是一样的

``` rails
params = {'bar' => 'baz'}
foo(params) #  ArgumentError: wrong number of arguments (1 for 0)
```

所以需要将 HashWithIndifferentAccess 转换成以 Symbol 作为 key

``` rails
params = {bar: 'baz'}.with_indifferent_access
foo(params.symbolize_keys) #  'baz'
```

> [返回目录](#目录)

## References

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

> [返回目录](#目录)
