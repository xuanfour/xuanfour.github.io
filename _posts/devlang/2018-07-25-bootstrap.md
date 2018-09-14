---
layout:     post
title:      "Bootstrap 4 学习"
date:       2015-07-13
categories: devlang
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - development language
    - web
    - bootstrap
---

# Bootstrap 4 学习

> * HTML 定义了网页的内容
> * CSS 描述了网页的布局
> * JavaScript 网页的行为

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Bootstrap 4 学习](#bootstrap-4-学习)
    - [目录](#目录)
    - [Bootstrap4](#bootstrap4)
        - [Bootstrap4 安装使用](#bootstrap4-安装使用)
            - [Bootstrap 4 CDN](#bootstrap-4-cdn)
            - [样例模版](#样例模版)
            - [下载 Bootstrap 4](#下载-bootstrap-4)
            - [创建第一个 Bootstrap 4 页面](#创建第一个-bootstrap-4-页面)
                - [添加 HTML5 doctype](#添加-html5-doctype)
                - [移动设备优先](#移动设备优先)
                - [容器类](#容器类)
                - [两个 Bootstrap 4 页面](#两个-bootstrap-4-页面)
        - [Bootstrap4 网格系统](#bootstrap4-网格系统)
            - [网格类](#网格类)
            - [网格系统规则](#网格系统规则)
                - [Bootstrap4 网格系统规则:](#bootstrap4-网格系统规则)
            - [Bootstrap 4 网格的基本结构](#bootstrap-4-网格的基本结构)
            - [不等宽响应式列](#不等宽响应式列)
            - [平板和桌面端](#平板和桌面端)
            - [平板、桌面、大桌面显示器、超大桌面显示器](#平板桌面大桌面显示器超大桌面显示器)
            - [偏移列](#偏移列)
        - [Bootstrap4 文字排版](#bootstrap4-文字排版)
            - [Bootstrap 4 默认设置](#bootstrap-4-默认设置)
            - [`<h1> - <h6>`](#h1---h6)
            - [Display 标题类](#display-标题类)
            - [`<small>`](#small)
            - [`<mark>`](#mark)
            - [`<abbr>`](#abbr)
            - [`<blockquote>`](#blockquote)
            - [`<dl>`](#dl)
            - [`<code>`](#code)
            - [`<kbd>`](#kbd)
            - [`<pre>`](#pre)
            - [更多排版类](#更多排版类)
        - [Bootstrap4 按钮](#bootstrap4-按钮)
            - [按钮设置边框](#按钮设置边框)
            - [不同大小的按钮](#不同大小的按钮)
            - [块级按钮](#块级按钮)
            - [激活和禁用的按钮](#激活和禁用的按钮)
        - [Bootstrap4 分页](#bootstrap4-分页)
            - [当前页页码状态](#当前页页码状态)
            - [分页显示大小](#分页显示大小)
        - [Bootstrap4 表单](#bootstrap4-表单)
            - [Bootstrap4 表单布局](#bootstrap4-表单布局)
            - [堆叠表单](#堆叠表单)
            - [内联表单](#内联表单)
        - [Bootstrap4 表单控件](#bootstrap4-表单控件)
            - [Bootstrap Input](#bootstrap-input)
            - [Bootstrap textarea](#bootstrap-textarea)
            - [Bootstrap 复选框(checkbox)](#bootstrap-复选框 checkbox)
            - [Bootstrap 单选框(Radio)](#bootstrap-单选框 radio)
            - [Bootstrap select 下拉菜单](#bootstrap-select-下拉菜单)
        - [Bootstrap4 轮播](#bootstrap4-轮播)
            - [如何创建轮播](#如何创建轮播)
            - [轮播图片上添加描述](#轮播图片上添加描述)
            - [以上实例中使用的类说明](#以上实例中使用的类说明)
    - [References](#references)

<!-- markdown-toc end -->

## Bootstrap4

### Bootstrap4 安装使用

我们可以通过以下两种方式来安装 Bootstrap4：

* 使用 Bootstrap 4 CDN。
* 从官网 getbootstrap.com 下载 Bootstrap 4。

#### Bootstrap 4 CDN

国内推荐使用 BootCDN 上的库：

Bootstrap4 CDN

```html
<!-- 官方 -->
<!-- CSS only -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

<!-- JS, Popper.js, and jQuery -->
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>

<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>

<!-- 国内推荐 -->
<!-- 新 Bootstrap4 核心 CSS 文件 -->
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.1.1/css/bootstrap.min.css">

<!-- jQuery 文件。务必在 bootstrap.min.js 之前引入 -->
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>

<!-- popper.min.js 用于弹窗、提示、下拉菜单 -->
<script src="https://cdn.bootcss.com/popper.js/1.12.5/umd/popper.min.js"></script>

<!-- 最新的 Bootstrap4 核心 JavaScript 文件 -->
<script src="https://cdn.bootcss.com/bootstrap/4.1.0/js/bootstrap.min.js"></script>
```

此外，你还可以使用以下的 CDN 服务：

* 国内推荐使用 : https://www.staticfile.org/
* 国际推荐使用：https://cdnjs.com/

#### 样例模版

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.3/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
  </body>
</html>
```

#### 下载 Bootstrap 4

你可以去官网 https://getbootstrap.com/ 下载 Bootstrap4 资源库。

注：此外你还可以通过包的管理工具 npm、gem、composer 等来安装：

```bash
npm install bootstrap
gem install bootstrap -v 4.1.3
composer require twbs/bootstrap:4.1.3
```

#### 创建第一个 Bootstrap 4 页面

##### 添加 HTML5 doctype

Bootstrap 要求使用 HTML5 文件类型，所以需要添加 HTML5 doctype 声明。
HTML5 doctype 在文档头部声明，并设置对应编码:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
</html>
```

##### 移动设备优先

为了让 Bootstrap 开发的网站对移动设备友好，确保适当的绘制和触屏缩放，需要在网页的 head 之中添加 viewport meta 标签，如下所示：

```html
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
```

* width=device-width 表示宽度是设备屏幕的宽度。
* initial-scale=1 表示初始的缩放比例。
* shrink-to-fit=no 自动适应手机屏幕的宽度。

##### 容器类

Bootstrap 4 需要一个容器元素来包裹网站的内容。
我们可以使用以下两个容器类：

* .container 类用于固定宽度并支持响应式布局的容器。
* .container-fluid 类用于 100% 宽度，占据全部视口（viewport）的容器。

##### 两个 Bootstrap 4 页面

Bootstrap4 .container 实例

```html
<div class="container">
  <h1>我的第一个 Bootstrap 页面</h1>
  <p>这是一些文本。</p>
</div>
```

以下实例展示了占据全部视口（viewport）的容器。
Bootstrap4 .container-fluid 实例

```html
<div class="container-fluid">
  <h1>我的第一个 Bootstrap 页面</h1>
  <p>使用了 .container-fluid，100% 宽度，占据全部视口（viewport）的容器。</p>
</div>
```

> [返回目录](#目录)

### Bootstrap4 网格系统

Bootstrap 提供了一套响应式、移动设备优先的流式网格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多 12 列。
我们也可以根据自己的需要，定义列数：
Bootstrap 4 的网格系统是响应式的，列会根据屏幕大小自动重新排列。

#### 网格类

Bootstrap 4 网格系统有以下 5 个类:

* .col- 针对所有设备
* .col-sm- 平板 - 屏幕宽度等于或大于 576px
* .col-md- 桌面显示器 - 屏幕宽度等于或大于 768px)
* .col-lg- 大桌面显示器 - 屏幕宽度等于或大于 992px)
* .col-xl- 超大桌面显示器 - 屏幕宽度等于或大于 1200px)

#### 网格系统规则

##### Bootstrap4 网格系统规则:

* 网格每一行需要放在设置了 .container (固定宽度) 或 .container-fluid (全屏宽度) 类的容器中，这样就可以自动设置一些外边距与内边距。
* 使用行来创建水平的列组。
* 内容需要放置在列中，并且只有列可以是行的直接子节点。
* 预定义的类如 .row 和 .col-sm-4 可用于快速制作网格布局。
* 列通过填充创建列内容之间的间隙。 这个间隙是通过 .rows 类上的负边距设置第一行和最后一列的偏移。
* 网格列是通过跨越指定的 12 个可用列来创建。 例如，设置三个相等的列，需要使用用三个.col-sm-4 来设置。
* Bootstrap 3 和 Bootstrap 4 最大的区别在于 Bootstrap 4 现在使用 flexbox（弹性盒子） 而不是浮动。Flexbox 的一大优势是，没有指定宽度的网格列将自动设置为等宽与等高列 。 如果您想了解有关 Flexbox 的更多信息，可以阅读我们的 CSS Flexbox 教程。

下表总结了 Bootstrap 网格系统如何在不同设备上工作的：

| 超小设备 <576pxn | 平板 ≥576px                    | 桌面显示器 ≥768px | 大桌面显示器 ≥992px | 超大桌面显示器 ≥1200px |          |
| ---------------- | -----------                    | ----------------- | ------------------- | ---------------------- |          |
| 容器最大宽度     | None(auto)                     | 540px             | 720px               | 960px                  | 1140px   |
| 类前缀           | .col-                          | .col-sm-          | .col-md-            | .col-lg-               | .col-xl- |
| 列数量和         | 12                             |                   |                     |                        |          |
| 间隙宽度         | 30px（一个列的每边分别 15px） |                   |                     |                        |          |
| 可嵌套           | Yes                            |                   |                     |                        |          |
| 列排序           | Yes                            |                   |                     |                        |          |

以下各个类可以一起使用，从而创建更灵活的页面布局。

#### Bootstrap 4 网格的基本结构

以下代码为 Bootstrap 4 网格的基本结构:
Bootstrap4 网格基本结构

```html
<!-- 第一个例子：控制列的宽度及在不同的设备上如何显示 -->
<div class="row">
  <div class="col-*-*"></div>
</div>
<div class="row">
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
  <div class="col-*-*"></div>
</div>

<!-- 第二个例子：或让 Bootstrap 者自动处理布局 -->
<div class="row">
  <div class="col"></div>
  <div class="col"></div>
  <div class="col"></div>
</div>
```

第一个例子：创建一行(`<div class="row">`)。然后， 添加是需要的列( .col-*-* 类中设置)。 第一个星号 (*) 表示响应的设备: sm, md, lg 或 xl, 第二个星号 (*) 表示一个数字, 同一行的数字相加为 12。

第二个例子: 不在每个 col 上添加数字，让 bootstrap 自动处理布局，同一行的每个列宽度相等： 两个 "col" ，每个就为 50% 的宽度。三个 "col"每个就为 33.33% 的宽度，四个 "col"每个就为 25% 的宽度，以此类推。同样，你可以使用 .col-sm|md|lg|xl 来设置列的响应规则。

接下来我们可以看看实例。

创建相等宽度的列，Bootstrap 自动布局

```html
<div class="row">
  <div class="col">.col</div>
  <div class="col">.col</div>
  <div class="col">.col</div>
</div>
```

等宽响应式列
以下实例演示了如何在平板及更大屏幕上创建等宽度的响应式列。 在移动设备上，即屏幕宽度小于 576px 时，四个列将会上下堆叠排版:

```html
<div class="col-sm-3">.col-sm-3</div>
<div class="col-sm-3">.col-sm-3</div>
<div class="col-sm-3">.col-sm-3</div>
<div class="col-sm-3">.col-sm-3</div>
```

#### 不等宽响应式列

以下实例演示了在平板及更大屏幕上创建不等宽度的响应式列。 在移动设备上，即屏幕宽度小于 576px 时，四个列将会上下堆叠排版:

```html
<div class="row">
  <div class="col-sm-4">.col-sm-4</div>
  <div class="col-sm-8">.col-sm-8</div>
</div>
```

#### 平板和桌面端

以下实例演示了在桌面设备的显示器上两个列的宽度各占 50%，如果在平板端则左边的宽度为 25%，右边的宽度为 75%, 在移动手机等小型设备上会堆叠显示。

```html
<div class="container-fluid">
  <div class="row">
    <div class="col-sm-3 col-md-6">
      <p>RUNOOB</p>
    </div>
    <div class="col-sm-9 col-md-6">
      <p>菜鸟教程</p>
    </div>
  </div>
</div>
```

#### 平板、桌面、大桌面显示器、超大桌面显示器

以下实例在平板、桌面、大桌面显示器、超大桌面显示器的宽度比例为分别为：25%/75%、50%/50%、33.33%/66.67%、16.67/83.33%, 在移动手机等小型设备上会堆叠显示。

```html
<div class="container-fluid">
  <div class="row">
    <div class="col-sm-3 col-md-6 col-lg-4 col-xl-2">
      <p>RUNOOB</p>
    </div>
    <div class="col-sm-9 col-md-6 col-lg-8 col-xl-10">
      <p>菜鸟教程</p>
    </div>
  </div>
</div>
```

#### 偏移列

偏移列通过 offset-*-* 类来设置。第一个星号( * )可以是 sm、md、lg、xl，表示屏幕设备类型，第二个星号( * )可以是 1 到 11 的数字。
为了在大屏幕显示器上使用偏移，请使用 .offset-md-* 类。这些类会把一个列的左外边距（margin）增加 * 列，其中 * 范围是从 1 到 11。
例如：.offset-md-4 是把.col-md-4 往右移了四列格。

```html
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 offset-md-4">.col-md-4 .offset-md-4</div>
</div>
<div class="row">
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
</div>
<div class="row">
  <div class="col-md-6 offset-md-3">.col-md-6 .offset-md-3</div>
</div>
```

> [返回目录](#目录)

### Bootstrap4 文字排版

#### Bootstrap 4 默认设置

Bootstrap 4 默认的 font-size 为 16px, line-height 为 1.5。
默认的 font-family 为 "Helvetica Neue", Helvetica, Arial, sans-serif。
此外，所有的 `<p>` 元素 margin-top: 0、margin-bottom: 1rem (16px)。

#### `<h1> - <h6>`

Bootstrap 中定义了所有的 HTML 标题（h1 到 h6）的样式。请看下面的实例：

```html
<div class="container">
  <h1>h1 Bootstrap 标题 (2.5rem = 40px)</h1>
  <h2>h2 Bootstrap 标题 (2rem = 32px)</h2>
  <h3>h3 Bootstrap 标题 (1.75rem = 28px)</h3>
  <h4>h4 Bootstrap 标题 (1.5rem = 24px)</h4>
  <h5>h5 Bootstrap 标题 (1.25rem = 20px)</h5>
  <h6>h6 Bootstrap 标题 (1rem = 16px)</h6>
</div>
```

#### Display 标题类

Bootstrap 还提供了四个 Display 类来控制标题的样式: .display-1, .display-2, .display-3, .display-4。

```html
<div class="container">
  <h1>Display 标题</h1>
  <p>Display 标题可以输出更大更粗的字体样式。</p>
  <h1 class="display-1">Display 1</h1>
  <h1 class="display-2">Display 2</h1>
  <h1 class="display-3">Display 3</h1>
  <h1 class="display-4">Display 4</h1>
</div>
```

#### `<small>`

在 Bootstrap 4 中 HTML <small> 元素用于创建字号更小的颜色更浅的文本:

```html
<div class="container">
  <h1>更小文本标题</h1>
  <p>small 元素用于字号更小的颜色更浅的文本:</p>
  <h1>h1 标题 <small>副标题</small></h1>
  <h2>h2 标题 <small>副标题</small></h2>
  <h3>h3 标题 <small>副标题</small></h3>
  <h4>h4 标题 <small>副标题</small></h4>
  <h5>h5 标题 <small>副标题</small></h5>
  <h6>h6 标题 <small>副标题</small></h6>
</div>
```

#### `<mark>`

Bootstrap 4 定义 <mark> 为黄色背景及有一定的内边距:

```html
<div class="container">
  <h1>高亮文本</h1>
  <p>使用 mark 元素来 <mark>高亮</mark> 文本。</p>
</div>
```

#### `<abbr>`

Bootstrap 4 定义 HTML <abbr> 元素的样式为显示在文本底部的一条虚线边框:

```html
<div class="container">
  <h1>Abbreviations</h1>
  <p>The abbr element is used to mark up an abbreviation or acronym:</p>
  <p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>
</div>
```

#### `<blockquote>`

对于引用的内容可以在 <blockquote> 上添加 .blockquote 类 :

```html
<div class="container">
  <h1>Blockquotes</h1>
  <p>The blockquote element is used to present content from another source:</p>
  <blockquote class="blockquote">
    <p>For 50 years, WWF has been protecting the future of nature. The world's leading conservation organization, WWF works in 100 countries and is supported by 1.2 million members in the United States and close to 5 million globally.</p>
    <footer class="blockquote-footer">From WWF's website</footer>
  </blockquote>
</div>
```

#### `<dl>`

Bootstrap 4 定义 HTML <dl> 元素的样式如下:

```html
<div class="container">
  <h1>Description Lists</h1>
  <p>The dl element indicates a description list:</p>
  <dl>
    <dt>Coffee</dt>
    <dd>- black hot drink</dd>
    <dt>Milk</dt>
    <dd>- white cold drink</dd>
  </dl>
</div>
```

#### `<code>`

Bootstrap 4 定义 HTML <code> 元素的样式如下:

```html
<div class="container">
  <h1>代码片段</h1>
  <p>可以将一些代码元素放到 code 元素里面:</p>
  <p>以下 HTML 元素: <code>span</code>, <code>section</code>, 和 <code>div</code> 用于定义部分文档内容。</p>
</div>
```

#### `<kbd>`

Bootstrap 4 定义 HTML <kbd> 元素的样式如下:

```html
<div class="container">
  <h1>Keyboard Inputs</h1>
  <p>To indicate input that is typically entered via the keyboard, use the kbd element:</p>
  <p>Use <kbd>ctrl + p</kbd> to open the Print dialog box.</p>
</div>
```

#### `<pre>`

Bootstrap 4 定义 HTML <pre> 元素的样式如下:

```html
<div class="container">
<h1>Multiple Code Lines</h1>
<p>For multiple lines of code, use the pre element:</p>
<pre>
Text in a pre element
is displayed in a fixed-width
font, and it preserves
both      spaces and
line breaks.
</pre>
</div>
```

#### 更多排版类

下表提供了 Bootstrap4 更多排版类的实例：

| 类名                | 描述                                                                                                                                              |
| ------------------- | -------                                                                                                                                           |
| .font-weight-bold   | 加粗文本                                                                                                                                          |
| .font-weight-normal | 普通文本                                                                                                                                          |
| .font-weight-light  | 更细的文本                                                                                                                                        |
| .font-italic        | 斜体文本                                                                                                                                          |
| .lead               | 让段落更突出                                                                                                                                      |
| .small              | 指定更小文本 (为父元素的 85% )                                                                                                                    |
| .text-left          | 左对齐                                                                                                                                            |
| .text-center        | 居中                                                                                                                                              |
| .text-right         | 右对齐                                                                                                                                            |
| .text-justify       | 设定文本对齐,段落中超出屏幕部分文字自动换行                                                                                                       |
| .text-nowrap        | 段落中超出屏幕部分不换行                                                                                                                          |
| .text-lowercase     | 设定文本小写                                                                                                                                      |
| .text-uppercase     | 设定文本大写                                                                                                                                      |
| .text-capitalize    | 设定单词首字母大写                                                                                                                                |
| .initialism         | 显示在 `<abbr>` 元素中的文本以小号字体展示，且可以将小写字母转换为大写字母                                                                        |
| .list-unstyled      | 移除默认的列表样式，列表项中左对齐 ( `<ul>` 和 `<ol>` 中)。 这个类仅适用于直接子列表项 (如果需要移除嵌套的列表项，你需要在嵌套的列表中使用该样式) |
| .list-inline        | 将所有列表项放置同一行                                                                                                                            |
| .pre-scrollable     | 使 `<pre>` 元素可滚动，代码块区域最大高度为 340px,一旦超出这个高度,就会在 Y 轴出现滚动条                                                             |

> [返回目录](#目录)

### Bootstrap4 信息提示

提示框可以使用 .alert 类, 后面加上 .alert-success, .alert-info, .alert-warning, .alert-danger, .alert-primary, .alert-secondary, .alert-light 或 .alert-dark 类来实现:

| link            | info | color |
| ----            | ---- | ----- |
| alert-success   | 成功 | 绿色  |
| alert-info      | 信息 | 浅蓝  |
| alert-warning   | 警告 | 黄色  |
| alert-danger    | 错误 | 红色  |
| alert-primary   | 首选 | 深蓝  |
| alert-secondary | 次要 | 浅灰  |
| alert-light     | 高亮 | 亮白  |
| calert-dark     | 深灰 | 深灰  |

``` html
<div class="alert alert-success">
  <strong>成功!</strong> 指定操作成功提示信息。
</div>
```

#### 提示框添加链接 ####

提示框中在链接的标签上添加 alert-link 类来设置匹配提示框颜色的链接：

``` html
<div class="alert alert-success">
  <strong>成功!</strong> 你应该认真阅读 <a href="#" class="alert-link">这条信息</a>。
</div>
```

#### 关闭提示框 ####

我们可以在提示框中的 div 中添加 .alert-dismissable 类，然后在关闭按钮的链接上添加 class="close" 和 data-dismiss="alert" 类来设置提示框的关闭操作。

``` html
<div class="alert alert-success alert-dismissable">
  <button type="button" class="close" data-dismiss="alert">&times;</button>
  <strong>成功!</strong> 指定操作成功提示信息。
</div>
```

提示: &times; (×) 是 HTML 实体字符，来表示关闭操作，而不是字母 "x"。

#### 提示框动画 ####

.fade 和 .show 类用于设置提示框在关闭时的淡出和淡入效果：

``` html
<div class="alert alert-danger alert-dismissable fade show">
```

> [返回目录](#目录)

### Bootstrap4 按钮

Bootstrap 4 提供了不同样式的按钮。

```html
<button type="button" class="btn">基本按钮</button>
<button type="button" class="btn btn-primary">主要按钮</button>
<button type="button" class="btn btn-secondary">次要按钮</button>
<button type="button" class="btn btn-success">成功</button>
<button type="button" class="btn btn-info">信息</button>
<button type="button" class="btn btn-warning">警告</button>
<button type="button" class="btn btn-danger">危险</button>
<button type="button" class="btn btn-dark">黑色</button>
<button type="button" class="btn btn-light">浅色</button>
<button type="button" class="btn btn-link">链接</button>
```

按钮类可用于 `<a>`, `<button>`, 或 `<input>` 元素上:

```html
<a href="#" class="btn btn-info" role="button">链接按钮</a>
<button type="button" class="btn btn-info">按钮</button>
<input type="button" class="btn btn-info" value="输入框按钮">
<input type="submit" class="btn btn-info" value="提交按钮">
```

#### 按钮设置边框

```html
<button type="button" class="btn btn-outline-primary">主要按钮</button>
<button type="button" class="btn btn-outline-secondary">次要按钮</button>
<button type="button" class="btn btn-outline-success">成功</button>
<button type="button" class="btn btn-outline-info">信息</button>
<button type="button" class="btn btn-outline-warning">警告</button>
<button type="button" class="btn btn-outline-danger">危险</button>
<button type="button" class="btn btn-outline-dark">黑色</button>
<button type="button" class="btn btn-outline-light text-dark">浅色</button>
```

#### 不同大小的按钮

Bootstrap 4 可以设置按钮的大小：

```html
<button type="button" class="btn btn-primary btn-lg">大号按钮</button>
<button type="button" class="btn btn-primary">默认按钮</button>
<button type="button" class="btn btn-primary btn-sm">小号按钮</button>
```

#### 块级按钮

通过添加 .btn-block 类可以设置块级按钮：

```html
<button type="button" class="btn btn-primary btn-block">按钮 1</button>
```

#### 激活和禁用的按钮

按钮可设置为激活或者禁止点击的状态。

.active 类可以设置按钮是可用的，disabled 属性可以设置按钮是不可点击的。 注意 `<a>` 元素不支持 disabled 属性，你可以通过添加 .disabled 类来禁止链接的点击。

```html
<button type="button" class="btn btn-primary active">点击后的按钮</button>
<button type="button" class="btn btn-primary" disabled>禁止点击的按钮</button>
<a href="#" class="btn btn-primary disabled">禁止点击的链接</a>
```

> [返回目录](#目录)

### Bootstrap4 分页

网页开发过程，如果碰到内容过多，一般都会做分页处理。
Bootstrap 4 可以很简单的实现分页效果。
要创建一个基本的分页可以在 `<ul>` 元素上添加 .pagination 类。然后在 `<li>` 元素上添加 .page-item 类：:

```html
<ul class="pagination">
  <li class="page-item"><a class="page-link" href="#">Previous</a></li>
  <li class="page-item"><a class="page-link" href="#">1</a></li>
  <li class="page-item"><a class="page-link" href="#">2</a></li>
  <li class="page-item"><a class="page-link" href="#">3</a></li>
  <li class="page-item"><a class="page-link" href="#">Next</a></li>
</ul>
```

#### 当前页页码状态

当前页可以使用 .active 类来高亮显示：

```html
<ul class="pagination">
  <li class="page-item"><a class="page-link" href="#">Previous</a></li>
  <li class="page-item"><a class="page-link" href="#">1</a></li>
  <li class="page-item active"><a class="page-link" href="#">2</a></li>
  <li class="page-item"><a class="page-link" href="#">3</a></li>
  <li class="page-item"><a class="page-link" href="#">Next</a></li>
</ul>
```

不可点击的分页链接
.disabled 类可以设置分页链接不可点击:

```html
<ul class="pagination">
  <li class="page-item disabled"><a class="page-link" href="#">Previous</a></li>
  <li class="page-item"><a class="page-link" href="#">1</a></li>
  <li class="page-item"><a class="page-link" href="#">2</a></li>
  <li class="page-item"><a class="page-link" href="#">3</a></li>
  <li class="page-item"><a class="page-link" href="#">Next</a></li>
</ul>
```

#### 分页显示大小

可以将分页条目设置为不同的大小。

.pagination-lg 类设置大字体的分页条目，.pagination-sm 类设置小字体的分页条目:

```html
<ul class="pagination pagination-lg">
  <li class="page-item"><a class="page-link" href="#">Previous</a></li>
  <li class="page-item"><a class="page-link" href="#">1</a></li>
  <li class="page-item"><a class="page-link" href="#">2</a></li>
  <li class="page-item"><a class="page-link" href="#">3</a></li>
  <li class="page-item"><a class="page-link" href="#">Next</a></li>
</ul>

<ul class="pagination pagination-sm">
  <li class="page-item"><a class="page-link" href="#">Previous</a></li>
  <li class="page-item"><a class="page-link" href="#">1</a></li>
  <li class="page-item"><a class="page-link" href="#">2</a></li>
  <li class="page-item"><a class="page-link" href="#">3</a></li>
  <li class="page-item"><a class="page-link" href="#">Next</a></li>
</ul>
```

面包屑导航
.breadcrumb 和 .breadcrumb-item 类用于设置面包屑导航：

```html
<ul class="breadcrumb">
  <li class="breadcrumb-item"><a href="#">Photos</a></li>
  <li class="breadcrumb-item"><a href="#">Summer 2017</a></li>
  <li class="breadcrumb-item"><a href="#">Italy</a></li>
  <li class="breadcrumb-item active">Rome</li>
</ul>
```

> [返回目录](#目录)

### Bootstrap4 表单

在本章中，我们将学习如何使用 Bootstrap 创建表单。Bootstrap 通过一些简单的 HTML 标签和扩展的类即可创建出不同样式的表单。
表单元素 `<input>`, `<textarea>`, 和 `<select>` elements 在使用 .form-control 类的情况下，宽度都是设置为 100%。

#### Bootstrap4 表单布局

* 堆叠表单 (全屏宽度)：垂直方向
* 内联表单：水平方向

Bootstrap 提供了两种类型的表单布局:

#### 堆叠表单

以下实例使用两个输入框，一个复选框，一个提交按钮来创建堆叠表单：

```html
<form>
  <div class="form-group">
    <label for="email">Email address:</label>
    <input type="email" class="form-control" id="email">
  </div>
  <div class="form-group">
    <label for="pwd">Password:</label>
    <input type="password" class="form-control" id="pwd">
  </div>
  <div class="form-check">
    <label class="form-check-label">
      <input class="form-check-input" type="checkbox"> Remember me
    </label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

#### 内联表单

所有内联表单中的元素都是左对齐的。
注意：在屏幕宽度小于 576px 时为垂直堆叠，如果屏幕宽度大于等于 576px 时表单元素才会显示在同一个水平线上。
内联表单需要在 `<form>` 元素上添加 .form-inline 类。

以下实例使用两个输入框，一个复选框，一个提交按钮来创建内联表单：

```html
<form class="form-inline">
  <label for="email">Email address:</label>
  <input type="email" class="form-control" id="email">
  <label for="pwd">Password:</label>
  <input type="password" class="form-control" id="pwd">
  <div class="form-check">
    <label class="form-check-label">
      <input class="form-check-input" type="checkbox"> Remember me
    </label>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

> [返回目录](#目录)

### Bootstrap4 表单控件

Bootstrap4 支持以下表单控件：

* input
* textarea
* checkbox
* radio
* select

#### Bootstrap Input

Bootstrap 支持所有的 HTML5 输入类型: text, password, datetime, datetime-local, date, month, time, week, number, email, url, search, tel, 以及 color。
注意：: 如果 input 的 type 属性未正确声明，输入框的样式将不会显示。
以下实例使用两个 input 元素，一个是 text，一个是 password：

```html
<div class="form-group">
  <label for="usr">用户名:</label>
  <input type="text" class="form-control" id="usr">
</div>
<div class="form-group">
  <label for="pwd">密码:</label>
  <input type="password" class="form-control" id="pwd">
</div>
```

#### Bootstrap textarea

以下实例演示了 textarea 的样式。

```html
<div class="form-group">
  <label for="comment">评论:</label>
  <textarea class="form-control" rows="5" id="comment"></textarea>
</div>
```

#### Bootstrap 复选框(checkbox)

复选框用于让用户从一系列预设置的选项中进行选择，可以选一个或多个。
以下实例包含了三个选项。最后一个是禁用的：

```html
<div class="form-check">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="">Option 1
  </label>
</div>
<div class="form-check">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="">Option 2
  </label>
</div>
<div class="form-check disabled">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="" disabled>Option 3
  </label>
</div>
```

使用 .form-check-inline 类可以让选项显示在同一行上：

```html
<div class="form-check form-check-inline">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="">Option 1
  </label>
</div>
<div class="form-check form-check-inline">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="">Option 2
  </label>
</div>
<div class="form-check form-check-inline disabled">
  <label class="form-check-label">
    <input type="checkbox" class="form-check-input" value="" disabled>Option 3
  </label>
</div>
```

#### Bootstrap 单选框(Radio)

复选框用于让用户从一系列预设置的选项中进行选择，只能选一个。
以下实例包含了三个选项。最后一个是禁用的：

```html
<div class="radio">
  <label><input type="radio" name="optradio">Option 1</label>
</div>
<div class="radio">
  <label><input type="radio" name="optradio">Option 2</label>
</div>
<div class="radio disabled">
  <label><input type="radio" name="optradio" disabled>Option 3</label>
</div>
```

使用 .radio-inline 类可以让选项显示在同一行上：

```html
<label class="radio-inline"><input type="radio" name="optradio">Option 1</label>
<label class="radio-inline"><input type="radio" name="optradio">Option 2</label>
<label class="radio-inline"><input type="radio" name="optradio">Option 3</label>
```

#### Bootstrap select 下拉菜单

当您想让用户从多个选项中进行选择，但是默认情况下只能选择一个选项时，则使用选择框。
以下实例包含了两个下拉菜单：

```html
<div class="form-group">
  <label for="sel1">下拉菜单:</label>
  <select class="form-control" id="sel1">
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
  </select>
</div>
```

> [返回目录](#目录)

### Bootstrap4 轮播

轮播是一个循环的幻灯片：

#### 如何创建轮播

以下实例创建了一个简单的图片轮播效果 ：

```html
<div id="demo" class="carousel slide" data-ride="carousel">

  <!-- 指示符 -->
  <ul class="carousel-indicators">
    <li data-target="#demo" data-slide-to="0" class="active"></li>
    <li data-target="#demo" data-slide-to="1"></li>
    <li data-target="#demo" data-slide-to="2"></li>
  </ul>

  <!-- 轮播图片 -->
  <div class="carousel-inner">
    <div class="carousel-item active">
      <img src="https://static.runoob.com/images/mix/img_fjords_wide.jpg">
    </div>
    <div class="carousel-item">
      <img src="https://static.runoob.com/images/mix/img_nature_wide.jpg">
    </div>
    <div class="carousel-item">
      <img src="https://static.runoob.com/images/mix/img_mountains_wide.jpg">
    </div>
  </div>

  <!-- 左右切换按钮 -->
  <a class="carousel-control-prev" href="#demo" data-slide="prev">
    <span class="carousel-control-prev-icon"></span>
  </a>
  <a class="carousel-control-next" href="#demo" data-slide="next">
    <span class="carousel-control-next-icon"></span>
  </a>

</div>
```

#### 轮播图片上添加描述

在每个 `<div class="carousel-item">` 内添加 `<div class="carousel-caption">` 来设置轮播图片的描述文本：:

```html
<div class="carousel-item">
  <img src="https://static.runoob.com/images/mix/img_fjords_wide.jpg">
  <div class="carousel-caption">
    <h3>第一张图片描述标题</h3>
    <p>描述文字!</p>
  </div>
</div>
```

#### 以上实例中使用的类说明

| 类                          | 描述                                                                                 |
| --------------------------- | ----                                                                                 |
| .carousel                   | 创建一个轮播                                                                         |
| .carousel-indicators        | 为轮播添加一个指示符，就是轮播图底下的一个个小点，轮播的过程可以显示目前是第几张图。 |
| .carousel-inner             | 添加要切换的图片                                                                     |
| .carousel-item              | 指定每个图片的内容                                                                   |
| .carousel-control-prev      | 添加左侧的按钮，点击会返回上一张。                                                   |
| .carousel-control-next      | 添加右侧按钮，点击会切换到下一张。                                                   |
| .carousel-control-prev-icon | 与 .carousel-control-prev 一起使用，设置左侧的按钮                                   |
| .carousel-control-next-icon | 与 .carousel-control-next 一起使用，设置右侧的按钮                                   |
| .slide                      | 切换图片的过渡和动画效果，如果你不需要这样的效果，可以删除这个类。                   |

> [返回目录](#目录)

## References

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出的或有不妥，请联系我立即增补或删除。

* <http://www.runoob.com/>

> [返回目录](#目录)