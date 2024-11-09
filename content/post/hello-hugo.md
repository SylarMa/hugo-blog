---
title:       "手把手教你零基础零费用使用Hugo+GitHub打造专属个人博客"
subtitle:    ""
description: ""
date:        2024-11-08
author:      "Pig Logic Park Studio"
image:       ""
tags:        ["Hugo", "快速入门"]
categories:  ["Hugo" ]
---
写这篇文章的原因是在网上看了很多的教程，踩了不少的坑，白费了很多功夫，也没找到一篇从头到尾完整有效的个人建站方法。

有些教程年代久远，有些教程极为繁琐，有些教程压根跑不通。

为了方便自己，做个记录，也方便大家，在这个人人都可以发声的时代，又感觉人人的喉咙都被扼住了。

虽然大家在各个媒体平台都有自己的账号，但是给自己留一份自己的自留地，貌似也不会是什么坏事。

这也是我建个人博客的最主要理由，因为有些东西因为这样的或者那样的原因，无法在公域平台发布，那么自己的博客网站，总可以容纳的下。

这是一套非常简单的方法，我希望可以让每一个人都可以照着这套方法建立自己的博客。

## 前置准备

--------------------------Mac 和 linux--------------------------

mac 和 linux： homebrew，git包管理，Node.js, vscode(推荐)

homebrew安装：直接命令行输入
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
git包管理：直接命令行输入
```
brew install git
```
Node.js: 下载安装包后按照默认设置安装

[Node.js](https://nodejs.org/en/download/)

--------------------------Windows--------------------------

windows：git包管理，hugo预编译文件，Node.js, vscode(推荐)

git包管理：点击下面链接下载后安装

https://github.com/git-for-windows/git/releases/download/v2.37.2.windows.2/Git-2.37.2.2-64-bit.exe

Node.js: 下载安装包后按照默认设置安装

[Node.js](https://nodejs.org/en/download/)

## 准备 hugo 环境

我们用hugo来写个人博客，首先得在本地安装hugo环境

----------------------------Windows环境----------------------------

windows：https://www.gohugo.org/doc/tutorials/installing-on-windows/

记得把hugo添加到环境变量中

----------------------------Mac OS环境----------------------------

Mac OS：命令行输入
```
brew install hugo
```
## 创建博客

1. 学会在命令行中创建blog（注意每一步命令输入后按「回车键」）

windows：在搜索栏中输入cmd或者命令行

mac：找到Terminal

2. 用命令行使用hugo创建一个blog项目（注意每一步命令输入后按「回车键」）

hugo new site 功能来创建一个新的blog，hugoblog这个名字可以根据自己的需要改
```
hugo new site hugoblog
```

3. cd hugoblog 进入刚刚创建好的博客地址中
```
cd hugoblog
```
## 添加主题

1. 给博客加个皮肤，一次复制+粘贴三行代码到命令行中

第一行：把当前目录进行初始化
```
git init  
```
第二行：下载anatole主题，并存放在themes文件夹中
```
git submodule add https://github.com/lxndrblz/anatole.git themes/anatole  
```
第三行：把主题改为anatole
```
echo theme = "anatole" >> config.toml
```
## 写博客

1. 写第一篇blog

hugo new + aaa/bbb.md， aaa指代的是某一个文件夹，如果你想写美食和电影两种，那就是[美食/第一篇美食.md]，或者[电影/第一篇电影.md]，尽量都用字母，其次一定要加.md
```
hugo new life/first_day.md
```
## 运行博客

1. 运行下博客看是否可行
```
hugo server
```
出现以下界面后，打开任意浏览器，输入http://localhost:1313 或者红框内的url都可以查看。

浏览器中出现博客界面说明你成功了

2. 生成静态文件，准备进一步托管
```
hugo -D
```
你可以去自己的文件目录中看到，public文件夹里面已经多了很多文件出来。

## 使用github pages进行托管

前提：准备一个github仓库，登录GitHub.com，注册账号，进入首页，点击New Repositories，输入项目名称，例如hugoblog

1. 在本地git bash命令行中进行git 初始化
```git init```

2. 检查是否有改变
```git status```

3. 提交到暂存区
```git add .```

4. 提交到版本库
```git commit -m "msg"```
  
5. 创建分支
```
git branch -M main
git remote add origin https://.....git
```

6. 推送到远程仓库
```git push -u origin main```

7. github pages部署设置

新建一个文件，在hugoblog目录下，名称为.github,然后在.github文件夹下新建一个文件夹workflows，在workflows文件夹下新建一个文件叫gh-pages.yml

总的路径为hugoblog/.github/workflows/gh-pages.yml

在gh-pages.yml输入以下内容后保存。
```
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.137.1
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb          
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          HUGO_CACHEDIR: ${{ runner.temp }}/hugo_cache
          HUGO_ENVIRONMENT: production
          TZ: America/Los_Angeles
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"          
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
8. 因为我们新建了文件，所以我们要把所有的文件都上传到github中。

再走一遍
```
git status 
git add . 
git commit -m "add yml file" 
git push
```
9. 成功的话，我们会发现所有的内容都上传到github了

10. 找到刚刚的github仓库，点击Actions，就可以看到我们的网站部署成功了。

11. 修改branch为main，位置在settings->Pages那里
Branch:main->/(root)

12. 最后一步，修改hugo的baseURL。

在github的仓库中找到Settings->Pages，找到为https://**.http://github.io/hugoblog

复制粘贴，打开config.toml，然后替换到原先的，当然，这里可以改成你自己的域名，更方便记忆。

在github的仓库中找到Settings->Pages，找到Custom domain，添加域名并保存。

域名解析到github即可。

再走一遍
```
git status 
git add . 
git commit -m "add new file" 
git push 
```

以后再写东西都重新走一遍git流程就好了。