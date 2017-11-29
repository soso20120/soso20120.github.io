---
layout: post 
title: "URI and URL"
date: 2017-07-13 11:21:51 +0800
categories: [Web]
excerpt: 这是一个学习Jekyll及搭建blog的经验过程。不断更新。
tags:
  - Web
---

## What is URI and URL?
---

###### 🔅 URI = Universal Resource Identifier 统一资源标志符
&emsp;在某一规则下能把一个资源独一无二地标识出来

###### 🔅 URL = Universal Resource Locator 统一资源定位符
&emsp;在某一协议下，以位置来标识

###### 🔅 关系：每个 URL 都是 URI

在Java类库中，URI类不包含任何访问资源的方法，它唯一的作用就是解析。

相反的是，URL类可以打开一个到达资源的流。但是需要协议支持，例如http，https，ftp，本地文件系统(file)和Jar文件(jar)。

###### 🔅 例子

**URI**


在HttpServer中，public void handle（final HttpExchange exchange）throws Exception方法，根据exchange对象可以拿到访问Http请求的URI对象

ps：`http://127.0.0.1:8080/cmd_helloworld/?name=guowuxin`

此时URI uri = exchange.getRequestURI()；

通过uri可以拿到连接的各部分内容： 

uri.getPath()--------------------> /cmd_helloworld 注意有斜杠

uri.getQuery()----------------------> name=guowuxin



