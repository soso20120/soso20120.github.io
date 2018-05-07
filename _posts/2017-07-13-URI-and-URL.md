---
layout: post 
title: "URI and URL"
date: 2017-07-13 11:21:51 +0800
categories: [Web]
excerpt: URI和URL的差别和用法。
tags:
  - Web
  - URL
  - URI
---

### Content

* content
{:toc}

## What is URI and URL?
---

###### 🔅 URI = Universal Resource Identifier 统一资源标志符
&emsp;在某一规则下能把一个资源独一无二地标识出来。

###### 🔅 URL = Universal Resource Locator 统一资源定位符
&emsp;在某一协议下，以位置来标识，说明要如何访问这个资源。

###### 🔅 关系：每个 URL 都是 URI

&emsp;在Java类库中，URI类不包含任何访问资源的方法，它唯一的作用就是解析。

&emsp;相反的是，URL类可以打开一个到达资源的流。但是需要协议支持，例如http，https，ftp，本地文件系统(file)和Jar文件(jar)。

###### 🔅 例子

**URI**

&emsp;在HttpServer中，public void handle（final HttpExchange exchange）throws Exception方法，根据exchange对象可以拿到访问Http请求的URI对象

>ps：`http://127.0.0.1:8080/cmd_helloworld/?name=guowuxin`
>
>此时URI uri = exchange.getRequestURI()；
>
>通过uri可以拿到连接的各部分内容： 
>
>uri.getPath()--------------------> `/cmd_helloworld` 注意有斜杠
>
>uri.getQuery()----------------------> `name=guowuxin`

**URL**

`http://example.org/absolute/URI/with/absolute/path/to/resource.txt`

`ftp://example.org/resource.txt`

## URL表示路径
---

###### 🔅 /和\

* `Unix`使用斜杆`/`作为路径分隔符，而web应用最新使用在Unix系统上面，所以目前所有的网络地址都采用`/`作为分隔符。
* `Windows`由于使用斜杆`/`作为`DOS命令提示符的参数标志`了，为了不混淆，所以采用反斜杠`\`作为`路径分隔符`。所以目前windows系统上的文件浏览器都是用`\` 作为路径分隔符。
* 随着发展，DOS系统已经被淘汰了，命令提示符也用的很少，斜杆和反斜杠在大多数情况下可以互换，没有影响。

###### 🔅 例子

```
./src/		//当前目录中的src文件夹
../src/		//当前目录中的上一层中的src文件夹
/src/		//项目根目录的磁盘文件夹
```
