---
title:       "Hugo博客使用Algolia添加搜索功能"
subtitle:    ""
description: ""
date:        2024-11-09
author:      "Pig Logic Park Studio"
image:       ""
tags:        ["Hugo", "Algolia", "搜索"]
categories:  ["Hugo" ]
---
可以使用 algolia 搜索，因为它无需占用服务器资源，而且提供的免费使用次数也足够多。
下文将以 LoveIt 主题为例，添加 algolia 搜索功能。
## algolia 官网上的配置
### 注册 algolia 账号
algolia 的官网：https://www.algolia.com
注册比较简单，此处略。
### 创建新的应用及索引
登录首页后会显示Get Started页面，直接点右上角Skip for now跳过。

我们创建一个应用

进入首页后点击左下角Settings，选择Application，选择右上角Create Application创建新的应用，选择数据中心的所处地，我选择了美西，蓝色是免费的，灰色是收费的，然后点击同意协议，并创建应用。然后我们会跳转一个界面。

我们创建一个索引

首页点击Search，选择Index，输入索引名称，选择Create Index，创建索引完成。

创建索引完毕后，我们来到概述Overview，点击API Keys。（如果找不到API Keys，可以进入Settings，选择右侧Team and Access下的API Keys，选择对应的应用，就可以看到API Keys）

把前面三个Application ID,Search-Only API Key,Admin API Key给记录下来。

在config.toml中配置，由于不同主题配置不同，下列内容略有不同。
```
# 搜索配置   
[languages.zh-cn.params.search]     
  enable = true     
  # 搜索引擎的类型 ("lunr", "algolia")     
  type = "algolia"     
  # 文章内容最长索引长度     
  contentLength = 4000     
  # 搜索框的占位提示语     
  placeholder = ""     
  # 最大结果数目     
  maxResultLength = 10     
  # 结果内容片段长度     
  snippetLength = 50     
  # 搜索结果中高亮部分的 HTML 标签     
  highlightTag = "em"     
  # 是否在搜索索引中使用基于 baseURL 的绝对路径     
  absoluteURL = false     
  [languages.zh-cn.params.search.algolia]       
    #填你创建的索引的名称       
    index = "Your Index Name"       
    #填你的 Application ID       
    appID = "Your Application ID"       
    # 填你的 Search-Only API Key       
    searchKey = "Your Search-Only API Key"
```

## 本地Hugo的配置

### 索引文件的生成
一般来说当我们使用hugo命令后，public文件夹下会自动生成algolia.json文件。

### 索引文件的上传
注意：由于手动上传索引文件比较复杂，所以这里不讨论如何手动上传索引文件，只讨论自动上传，但若有需要可见这里 https://ieblyang.github.io/hugo-algolia/ 。
在我们本地 blog 站点的根目录下（我这里是D:\Hblog\site_name）执行以下命令：
```
npm init   
npm install atomic-algolia --save
```
执行完后会生成node_modules文件夹（如果代码托管在 GitHub 的话，可以在.gitignore中添加/node_modules以忽略该文件）。

我遇到的问题：在执行npm init后，终端会进入一个编辑模式，从而无法输入第二个命令。但是我发现在我的电脑中，直接使用第二个命令npm install atomic-algolia --save而不使用npm init，最后一样可用。

在项目根目录下还会有一个package.json文件，打开该文件，在scripts:{}中添加"algolia": "atomic-algolia"后结果如下：
```
"scripts": 
{   "test": "echo \"Error: no test specified\" && exit 1",
    "algolia": "atomic-algolia"    
  },
```
在 blog 项目根目录下建立一个.env文件，文件内容如下：（根据自己的值填，一般来说第三项不用改）
```
ALGOLIA_APP_ID=Your Application ID   
ALGOLIA_INDEX_NAME= Your Index Name   
ALGOLIA_INDEX_FILE=public/algolia.json   
ALGOLIA_ADMIN_KEY= Your Admin API Key
```
在 blog 项目根目录下执行下面的命令便可将索引文件自动上传至更新 algolia。
```
npm run algolia
```
### 索引文件的更新

在日后，我们每一次增添文章或修改文章后，都要再将索引文件上传以更新。一般来说，我们只要在blog项目根目录执行下面两行代码，便可以更新索引文件。

使索引文件 index.json 在文件夹 public 中生成
```
hugo
```
将索引文件上传
```
npm run algolia
```

https://ieblyang.github.io/hugo-algolia/