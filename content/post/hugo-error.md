---
title:       "Hugo Error"
subtitle:    ""
description: ""
date:        2024-11-07
author:      "Pig Logic Park Studio"
image:       ""
tags:        ["Hugo", "Error"]
categories:  ["Hugo" ]
---
# Hugo Error

1、git push SSL certificate problem: unable to get local issuer certificate
```
$ git push --set-upstream origin master
fatal: unable to access 'https://github.com/name/name.github.io.git/': SSL certificate problem: unable to get local issuer certificate
```
这个问题是由于没有配置信任的服务器HTTPS验证。默认，cURL被设为不信任任何CAs，就是说，它不信任任何服务器验证。
只需要执行下面命令就可以解决：
```
git config --global http.sslVerify false
```