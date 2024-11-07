---
title:       "Hello Hugo"
subtitle:    ""
description: ""
date:        2018-06-04
author:      ""
image:       ""
tags:        ["Hugo", "快速入门"]
categories:  ["Hugo" ]
---
# 快速入门

在几分钟内学会创建Hugo网站。
在本教程中，您将：

1、创建网站
2、添加内容
3、配置网站
4、发布网站

## 前提条件

开始本教程之前，您必须：

1、安装 Hugo（扩展版，版本 v0.112.0 或更高）(https://github.com/gohugoio/hugo/releases/latest)
2、安装 Git(https://git-scm.com/downloads)

您还必须熟悉使用命令行界面。

## 创建网站

### 命令

*如果您是Windows用户：*
**不要使用命令提示符**
**不要使用 Windows PowerShell**
**请在 PowerShell 或 Linux 终端（如WSL或Git Bash）中运行这些命令**
**PowerShell 和 Windows PowerShell 是不同的应用程序。**

运行以下命令，使用 Ananke 主题创建 Hugo 网站。下一部分将解释每个命令的用途。
```
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
echo "theme = 'ananke'" >> hugo.toml
hugo server
```
在终端中显示的 URL 中查看您的网站。按下 Ctrl + C 停止 Hugo 的开发服务器。

### 命令解释 
在 quickstart 目录中为您的项目创建 目录结构。
```hugo new site quickstart```

将当前目录更改为项目的根目录。
```cd quickstart```

在当前目录中初始化一个空的 Git 仓库。
```git init```

将 Ananke 主题克隆到 themes 目录中，并将其作为 Git 子模块 添加到您的项目中。
```git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke```

向站点配置文件中追加一行，指示当前使用的主题。
```echo "theme = 'ananke'" >> hugo.toml```

启动 Hugo 的开发服务器以查看网站。
```hugo server```

按下 Ctrl + C 停止 Hugo 的开发服务器。

## 添加内容

向您的网站添加一个新页面。
```hugo new content/posts/my-first-post.md```

Hugo 会在 content/posts 目录中创建该文件。使用编辑器打开该文件。
```
---
title: "我的第一篇文章"
date: 2022-11-20T09:03:20-08:00
draft: true
---
```
注意 [front matter] 中的 draft 值为 true。默认情况下，Hugo 在构建网站时不会发布草稿内容。

在文章正文中添加一些 [markdown]，但不要更改 draft 值。
```
---
title: "我的第一篇文章"
date: 2022-11-20T09:03:20-08:00
draft: true
---

简介

这是 **粗体** 文本，这是 *斜体* 文本。

访问 [Hugo](https://gohugo.io) 网站！
```
保存文件，然后启动 Hugo 的开发服务器以查看网站。您可以运行以下命令之一来包含草稿内容。
```
hugo server --buildDrafts
hugo server -D
```
在终端中显示的 URL 中查看您的网站。随着继续添加和更改内容，请保持开发服务器运行。

Hugo 的渲染引擎符合 CommonMark 的 规范。CommonMark 组织提供了一个由参考实现驱动的有用的 实时测试工具。

## 配置网站

使用编辑器打开项目根目录下的 网站配置 文件（hugo.toml）。
```
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = '我的新 Hugo 网站'
theme = 'ananke'
```
进行以下更改：

为您的生产网站设置 baseURL。该值必须以协议开头，并以斜杠结尾，如上所示。

将 languageCode 设置为您的语言和地区。

为您的生产网站设置 title。

启动 Hugo 的开发服务器以查看您的更改，记得包含草稿内容。

```hugo server -D```
大多数主题作者提供配置指南和选项。请务必访问您的主题的存储库或文档站点了解详细信息。

Ananke 主题的作者 The New Dynamic 提供了关于配置和使用的 文档。他们还提供了一个演示站点。

## 发布网站

在此步骤中，您将“发布”网站，但不会 “部署”它。

当您“发布”网站时，Hugo 会在项目根目录的 public 目录中创建整个静态网站。其中包括 HTML 文件和像图像、CSS 文件和 JavaScript 文件这样的资源。

当您发布网站时，通常不希望包含[草稿、将来或过期内容]。命令很简单。

```hugo```

要了解如何“部署”您的网站，请参阅托管和部署部分。