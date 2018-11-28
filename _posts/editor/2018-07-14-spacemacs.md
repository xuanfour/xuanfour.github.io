---
layout:     post
title:      "Spacemacs 学习"
date:       2015-07-14
categories: editor
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - spacemacs
---

> 本文是我的 Spacemacs 学习笔记

# Spacemacs 学习

## 目录

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Spacemacs 学习](#spacemacs-学习)
    - [目录](#目录)
    - [快捷键](#快捷键)
        - [控制键定义](#控制键定义)
        - [引导键配置](#引导键配置)
        - [重要快捷键](#重要快捷键)
        - [自定义快捷键](#自定义快捷键)
        - [shell 快捷键](#shell-快捷键)
        - [help 快捷键](#help-快捷键)
        - [text 快捷键](#text-快捷键)
        - [expand region 快捷键](#expand-region-快捷键)
        - [search/symbol 快捷键](#searchsymbol-快捷键)
            - [默认输入](#默认输入)
            - [命令](#命令)
            - [检索工具](#检索工具)
            - [作用域](#作用域)
            - [在当前文件中搜索](#在当前文件中搜索)
            - [搜索](#搜索)
        - [jump/join/split 快捷键](#jumpjoinsplit-快捷键)
        - [narrow/numbers](#narrownumbers)
        - [files 快捷键](#files-快捷键)
        - [toggles 快捷键](#toggles-快捷键)
        - [major-mode-cmd 快捷键](#major-mode-cmd-快捷键)
        - [other 快捷键](#other-快捷键)
    - [M-x 命令](#m-x-命令)
        - [进入命令的快捷键](#进入命令的快捷键)
    - [Project 设置](#project-设置)
    - [中英文混排空格 PanGu-Spacing](#中英文混排空格-pangu-spacing)
    - [设置缺省路径](#设置缺省路径)
    - [中文乱码](#中文乱码)
    - [环境变量](#环境变量)
    - [References](#references)

<!-- markdown-toc end -->

## 快捷键

### 控制键定义

| 控制键   | MacOS    | Windows  | 说明                            |
| -------- | -------- | -------- | ------------------------------- |
| (C)trl   | Control  | Ctrl     |                                 |
| (M)eta   | Option   | Alt      |                                 |
| (S)hift  | Shift    | Shift    |                                 |
| (s)uper  | Command  | Win      |                                 |
| (L)eader | custom   | custom   | Spacemacs 中一般为 <SPC> 空格键 |

### 引导键配置

| 引导键    | 配置选项                                 | 说明                            |
| ------    | -----                                    | -------                         |
| `<space>` | dotspacemacs-leader-key                  | vim 按键 leader 键              |
| ,         | dotspacemacs-major-mode-leader-key       | vim 按键 major-mode-leader 键   |
| :         | dotspacemacs-ex-command-key              | vim 按键扩展命令键              |
| M-m       | dotspacemacs-emacs-leader-key            | emacs 按键 leader 键            |
| C-M-m     | dotspacemacs-major-mode-emacs-leader-key | emacs 按键 major-mode-leader 键 |

### 重要快捷键

| 快捷键或命令                   | 说明                             |
| ------------------------------ | -------------------------------- |
| C-g                            | 停止当前运行/输入的命令          |
| C-x u                          | 撤销前一个命令                   |
| `M-x revert-buffer <Return>`   | 撤销上次存盘后所有改动           |
| `M-x recover-file <Return>`    | 从自动存盘文件恢复               |
| `M-x recover-session <Return>` | 如果你编辑了几个文件, 用这个恢复 |

### 自定义快捷键

| 快捷键 | evil 状态     | 说明     |
| ------ | ------------- | -------- |
| Q      | normal/visual | 查找替换 |

### shell 快捷键

| 快捷键       | 说明                                         |
| ------------ | -------------------------------------------- |
| :! command   | 执行 shell 命令，backspace 最小化 shell 窗格 |
| :r! command  | 执行 shell 命令，同时将结果粘贴到光标处      |
| L-!          | 执行 shell 命令，结果在小窗显示              |
| L-'          | 打开 shell 窗口                              |

### help 快捷键

| Leader | 控制键  | 其他键 | 说明                           |
| ------ | ------  | ------ | ----                           |
|        | C-h c   |        | 显示快捷键绑定的命令           |
| L-hdk  | C-h k   |        | 显示快捷键绑定的命令和它的作用 |
|        | C-h l   |        | 显示最后 100 个键入的内容      |
|        | C-h w   |        | 显示命令被绑定到哪些快捷键上   |
| L-hdf  | C-h f   |        | 显示函数的功能                 |
| L-hdv  | C-h v   |        | 显示变量的含义和值             |
|        | C-h m   |        | 显示当前缓冲区模式的帮助文档   |
|        | C-h b   |        | 显示当前缓冲区所有可用的快捷键 |
|        | C-h t   |        | 打开 emacs 教程                |
|        | C-h i   |        | 打开 info 阅读器               |
|        | C-h C-f |        | 显示 emacs FAQ                 |
|        | C-h p   |        | 显示本机 Elisp 包的信息        |

### text 快捷键

| Leader | 控制键 | 其他键 | 说明 |
| ------ | ------ | ------ | ---- |
| L-xU   |        |        | 大写 |
| L-xu   |        |        | 小写 |

### expand region 快捷键

| Leader | 控制键 | 其他键 | 说明                       |
| ------ | ------ | ------ | ----                       |
| L-vv   |        |        | 扩展文字区域               |
| L-vV   |        |        | 收缩文字区域               |
| L-vr   |        |        | 重置                       |
| L-ve   |        |        | 编辑                       |
| L-v/   |        |        | 从项目中检索文字区域       |
| L-vf   |        |        | 从文件中检索文字区域       |
| L-vb   |        |        | 从所有缓冲区中检索文字区域 |

### search/symbol 快捷键

#### 搜索 ####

| Leader | 控制键 | 其他键 | 说明                                 |
| ------ | ------ | ------ | ----                                 |
| *      |        |        | 搜索当前符号并向前跳转               |
| #      |        |        | 搜索当前符号并向后跳转               |
| L-sh   |        |        | 在当前范围内高亮当前符号的所有匹配项 |
| L-sH   |        |        | 转到最后的高亮当前符号事件           |
| L-se   |        |        | 高亮并编辑当前符号的所有匹配项       |
| L-sc   |        |        | 清除高亮                             |
| L-sj   |        |        | 检索并跳转到缓冲区符号               |

#### 默认输入 ####

默认输入指当前缓存的选择区域或光标下的关键字。

#### 命令 ####

Leader s 检索工具 作用域

#### 检索工具 ####

如果省略检索工具，则自动选择默认工具进行搜索。列表定义 `dotspacemacs-search-tools`，默认顺序是 ag、pt、ack、grep。

- a: ag
- t: pt
- k: ack
- g: grep

#### 作用域 ####

大写作用域键用默认输入来搜索。重复作用域键用来搜索当前文件。

- b：当前打开的所有缓存文件。
- p：当前项目下的文件。
- d：选择（默认当前）目录。
- f：选择（默认当前）目录下的文件。
- w：选择网络。

#### 在当前项目中搜索 ####

| Leader | 控制键 | 其他键 | 说明                     |
| ------ | ------ | ------ | ------------------------ |
| L-sp   |        |        | 在当前项目中搜索         |
| L-sP   |        |        | 在当前项目中搜索默认输入 |

当前项目搜索的二级菜单

| Leader    | 控制键 | 其他键 | 说明                          |
| ------    | ------ | ------ | ------------------------      |
| C-c C-l   |        |        | 搜索历史                      |
| C-c C-e   |        |        | 编辑搜索结果列表              |
| C-c <Tab> |        |        | 当前搜索结果添加到当前缓冲    |
| C-z       |        |        | helm actions 前缀键（可省略） |
| <F1>      |        |        | 打开文件                      |
| <F2>      |        |        | 在其他窗口打开文件            |
| <F3>      |        |        | 搜索结果列表保存到临时缓冲    |
| <F4>      |        |        | 编辑搜索结果列表              |

常见操作：
`L-sp` 在项目中搜索，显示搜索结果后按键 `<F4>` 编辑搜索结果列表，然后按键 `C-c C-c` 提交修改，或者按键 `C-c C-k`，然后回答 `y` 放弃修改。
也可以按键 `<F3>` 将搜索结果列表保存到临时缓冲后逐一修改。

#### 在当前文件中搜索 ####

| Leader | 控制键 | 其他键 | 说明                                |
| ------ | ------ | ------ | ------------------------            |
| L-ss   |        |        | 在当前文件中使用 swoop 搜索         |
| L-sS   |        |        | 在当前文件中使用 swoop 搜索默认输入 |
| L-saa  |        |        | 在当前文件中使用 ag 搜索            |
| L-saA  |        |        | 在当前文件中使用 ag 搜索默认输入    |
| L-sg   |        |        | 在当前文件中使用 grep 搜索          |
| L-sgG  |        |        | 在当前文件中使用 grep 搜索默认输入  |

### jump/join/split 快捷键

| Leader      | 控制键 | 其他键 | 说明                                          |
| ------      | ------ | ------ | ----                                          |
|             |        | %      | 跳转到对应语法位置                            |
| L-ji        |        |        | 检索并跳转到缓冲区符号                        |
| L-jj {char} |        |        | 检索 {char}，键入屏幕显示的自符跳转到对应位置 |

### narrow/numbers ###

| Leader | 控制键 | 其他键 | 说明                           |
| ------ | ------ | ------ | ----                           |
| L-nf   |        |        | 将缓冲区缩小到当前函数         |
| L-np   |        |        | 将缓冲区缩小到可见页面         |
| L-nr   |        |        | 将缓冲区缩小到所选文本         |
| L-nw   |        |        | 将缓冲区加宽，即还原整个缓冲区 |
| L-n=   |        |        | 增加文本数值                   |
| L-n-   |        |        | 减少文本数值                   |

### files 快捷键

| Leader | 控制键 | 其他键 | 说明         |
| ------ | ------ | ------ | ----         |
| L-ft   |        |        | 切换 neotree |

### window 快捷键

| Leader    | 控制键 | 其他键 | 说明                       |
| ------    | ------ | ------ | ----                       |
| L-1..9    |        |        | 切换 window                |
| L-w[hjkl] |        |        | 切换到上下左右 window      |
| L-w[HJKL] |        |        | 当前 window 移动到上下左右 |
| L-w-      |        |        | 上下分割 window            |
| L-w/      |        |        | 左右分割 window            |
| L-wd      |        |        | 关闭 window                |
| L-wb      |        |        | 切换到 minibuffer          |
|           |        |        |                            |

### toggles 快捷键

| Leader    | 控制键 | 其他键 | 说明               |
| ------    | ------ | ------ | -----------------  |
| L-t<Tab>  |        |        | 切换显示缩进辅助线 |
| L-tn      |        |        | 切换显示行号       |
| L-tr      |        |        | 切换显示相对行号   |
| L-tf      |        |        | 切换高亮 80 列     |
| L-t8      |        |        | 切换高亮长行       |
| L-t C-8   |        |        | 切换全局高亮长行   |
| L-tw      |        |        | 切换高亮空白       |
| L-tW      |        |        | 清除高亮空白       |
| L-t C-w   |        |        | 切换全局高亮空白   |
| L-t C-S-w |        |        | 清除全局高亮空白   |

### major-mode-cmd 快捷键

| Leader      | 控制键  | 其他键     | 说明                                          |
| ------      | ------  | ------     | ----                                          |
|             |         | ,          | major mode                                    |
| L-meb       |         | ,eb        | 执行当前 buffer                               |
| L-mee       | C-x C-e | ,ee        | 执行最后一条表达式，结果在小窗显示            |
| L-m=        |         | ,=         | 格式化代码                                    |

### other 快捷键

| Leader      | 控制键  | 其他键     | 说明                                          |
| ------      | ------  | ------     | ----                                          |
| `L-<Space>` | M-x     |            | M-x                                           |
| `L-<Tab>`   |         |            | 切换到上一个 buffer                           |
|             |         | `[<space>` | 增加行上空行                                  |
|             |         | `]<space>` | 增加行上空行                                  |
|             |         | ]]         | 在当前位置换行                                |
|             | C-x ;   |            | 设置注释列                                    |
| L-;;        | C-x C-; |            | 注释当前行                                    |
| L-;         |         |            | 注释选择行                                    |
|             | C-o/i   |            | 向上/下跳转到上次移动位置                     |
|             |         | ,          | major mode                                    |
|             | C-j     |            | 在光标处打印最后一条表达式结果                |
|             |         | =          | 格式化选择区域代码                            |

## M-x 命令 ##

### 进入命令的快捷键 ###

- M-x
- LL

- cd: 选择当前路径

> [返回目录](#目录)

## Project 设置 ##

如果是 git 项目，spacemacs 发现有 .git 目录，就会认为是一个 spacemacs project。
如果没有 .git 目录，就需要手动创建一个 .projectile 空文件，告诉 spacmeacs 此处是 project 根目录。

```bash
touch .projectile
```

> [返回目录](#目录)

## iedit ##

Spacemacs 使用强大的 iedit 模式通过 evil-iedit-state 多点位编辑语法关键字和选择区域。
evil-iedit-state 定义了两个新的 evil 状态：

- iedit state
- iedit-insert state

可以通过快捷键 `L-se` 和 `L-ve` 进入 iedit。进入 iedit 编辑状态后文本位置显示红色。iedit-insert state 必须按两次 ESC 才能回到正常状态。也可以随时按 C-g 返回正常状态。

| 快捷键 | 说明                                                            |
| ------ | ----                                                            |
| ESC    | 回到正常状态                                                    |
| TAB    | 切换当前区域的 iedit state 选中状态                             |
| 0      | 转到当前区域的开头                                              |
| $      | 转到当前区域的结尾                                              |
| #      | 为所有区域前缀一个增加的数字，SPC u# 来选择起始编号和文字格式。 |
| A      | 转到当前区域的结尾并切换到 iedit-insert state                   |
| D      | 删除所有区域                                                    |
| F      | 将范围限制                                                      |
| gg     | 去第一次区域                                                    |
| G      | 去最后一次区域                                                  |
| I      | 转到当前区域的开头并切换到 iedit-insert state                   |
| J      | 将编辑范围增加一行以下                                          |
| K      | 将编辑范围增加一行以上                                          |
| L      | 将范围限制为当前行                                              |
| n      | 去下一个区域                                                    |
| N      | 转到上一个区域                                                  |
| p      | 用最后复制的文本替换                                            |
| S      | 替换删除并切换到 iedit-insert state                             |
| V      | 切换所有区域以外的区域是否可见                                  |
| U      | 区域文字大写                                                    |
| C-U    | 区域文字小写                                                    |

> [返回目录](#目录)

## 中英文混排空格 PanGu-Spacing ##

需要在中英文混排的时候，在英文两边增加空格，可以增加 chinese layer，这个 layer 里包括一个 pangu-spacing 包，是用来更好地显示中英文混排的，默认情况下，中英文混排会在英文前后添加 1 个空格分割显示，保存的也时候也会写入到文件当中。

* 如果想在某个模式里禁用，可以在配置文件里把模式加入 pangu-spacing-inhibit-mode-alist。
* 如果想在当前 buffer 里切换，可以使用命令 pangu-spacing-mode。
* 如果想全局禁用，可以设置 global-pangu-spacing-mode。
* 这个设置并不会真正在文件中插入空白，如果你希望这样，配置 (setq pangu-spacing-real-insert-separtor t)

> [返回目录](#目录)

## 设置缺省路径 ##

* 增加 `(cd "/some/dir/")` 到配置文件的 `user-init` 方法。
* 使用钩子函数 `(add-hook 'find-file-hook #'(lambda () (setq default-directory (expand-file-name "/some/dir/"))))`。
* 在查找文件之前调用自定义函数 `(cd "/some/dir/")`。

> [返回目录](#目录)

## 中文乱码 ##

emacs 打开文件后常常因为默认编码与文档编码不同而显示为乱码。此时不用惊慌，只需 `C-x <RET> r ( M-x revert-buffer-with-coding-system)` 来用指定的编码重新读入这个文件即可。一般乱码都是因为 emacs 下使用 latin 或者 utf8，而打开的文档是 gb2312 编码。如果不记得编码类型就试一下，基本上 gb2312 都能解决。询问编码时记得用 tab 补齐比较方便。

另一种更方便的方法是使用 unicad，下载 unicad.el 保存到相应目录（譬如.emacs 中配置 my-elisp 文件夹为存放目录），然后在.emacs 中声明 `(require ‘unicad)` 即可。这样下次打开文档时会自动判断编码类型，非常方便。

> [返回目录](#目录)

## 环境变量 ##

可以通过 `~/.spacemacs.d/.spacemacs.env` 设置环境变量文件。

* 快捷键 `<leader>fee` 编辑环境变量文件。
* 快捷键 `<leader>fe C-e` 强制初始化环境变量文件。

## References

> 本文是我的学习笔记，内容参考了网上资源，为了方便自己查询使用，做了一些修改整理。
> 笔记内容摘录于下列文章，相应权利归属原作者，如有未列出或不妥，请联系我立即增补或删除。

> [返回目录](#目录)
