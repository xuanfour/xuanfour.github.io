---
layout:     post
title:      "Spacemacs 的工作空间（Layout、Perspective、Workspace）"
date:       2018-08-11
categories: editor
author:     "xuanfour"
header-img: "img/post-bg-unix-linux.jpg"
tags:
    - editor
    - emacs
    - spacemacs
---

> 本人原创文章，转载请在文章开始或结尾处标明作者和文章来源地址信息。

# Spacemacs 的工作空间（Layout、Perspective、Workspace）

Spacemacs 的工作空间功能其实挺强的，完全可以满足大多数程序猿和攻城狮的使用。只是 Layouts、Layout、Perspectives、Perspective、Workspace 这几个英文名称和他们在 Spacemacs 里所代表的具体含义是有差异的，太容易混淆大家的理解了。
经过多方查询资料，和自己的实际测试，我觉得真正的含义其实很简单： Layout/Perspective 和 Workspace 的实际含义和各自的英文语义正好是相反的！

## Layout 和 Perspective

Layout/Perspective，两个词其实是同一概念，表示一组相关联的 buffers 命名工作组。
可以使用 `<leader>pl` 将 project 切换为 layout，也可以使用 `<leader>ll` 或者 `<leader>l[1-9]` 选择或者新建一个 Layout。
Layouts 默认有一个名称为 `Default` 号码为 `1` 的缺省 Layout，包含所有的 buffer。

## Layouts 和 Perspectives

Layouts/Perspectives 是将多个工作组集合在一起的命名工作空间。
可以使用 `<leader>ls` 保存 layouts后，使用 `<leader>lL` 输入名称来打开一个 Layouts。

## Workspace

Workspace 是 Layout 的不同的视角，可以通过不同的 Workspace 使用不同的 Window 组合来工作。
可以使用 `<leader>lwc` 或者 `<leader>lw[1-9]` 选择或者新建一个 Workspace。
Workspace 默认有一个号码为 `1` 的缺省 Workspace。

## 显示与切换

Modeline 最左侧向右依次显示 Layout 名称、Workspace 名称/号码（如果只有一个则不显示）、窗口号。在装入 Layouts 后，可以使用快捷键达到快速切换工作场景的目标。

* `<leader>lL`      装入工作空间（Layouts/Perspectives）。
* `<leader>l[1-9]`  切换工作组（Layout/Perspective）。
* `<leader>lw[1-9]` 切换编辑视角（Workspace）。
* `<leader>[1-9]`   切换编辑窗口（Window）。

> [返回目录](#目录)
