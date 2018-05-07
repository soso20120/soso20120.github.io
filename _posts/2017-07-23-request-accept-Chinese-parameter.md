---
layout: post 
title: "Request如何接收表单的中文参数"
date: 2017-07-23 10:14:15 +0800
categories: [Web]
excerpt: Request接收表单提交中文参数乱码问题，使用的语言为JAVA。
tags:
  - Web
  - JAVA
  - Request
  - 中文乱码
  - 后台
---

### Content

* content
{:toc}

### 1.产生乱码的原因

&emsp;之所以会产生乱码，就是因为服务器和客户端沟通的编码不一致造成的，因此解决的办法是：在客户端和服务器之间设置一个统一的编码，之后就按照此编码进行数据的传输和接收。

&emsp;由于客户端是以`UTF-8`字符编码将表单数据传输到服务器端的，因此服务器也需要设置以UTF-8字符编码进行接收，要想完成此操作，服务器可以直接使用从`ServletRequest`接口继承而来的`setCharacterEncoding(charset)`方法进行统一的编码设置。

### 2.对于POST请求

```java
public void doPost(HttpServletRequest request, HttpServletResponse response)
	throws ServletException, IOException {
	request.setCharacterEncoding("UTF-8");
	String userName = request.getParameter("userName");
	}
```

### 3.对于GET请求

>Request即使设置了以指定的编码接收数据也是无效的，还是默认使用ISO8859-1这个字符编码来接收数据。<br>
>在接收到数据后，先获取request对象以ISO8859-1字符编码接收到的原始数据的字节数组，然后通过字节数组以指定的编码构建字符串，解决乱码问题。

```java
public void doGet(HttpServletRequest request, HttpServletResponse response)
	throws ServletException, IOException {
		String name = request.getParameter("name");//接收数据
        name =new String(name.getBytes("ISO8859-1"), "UTF-8") ;
	}
```

>实际上拆为两步

```java
byte[] source = name.getBytes("ISO8859-1");
name = new String(source, "UTF-8");
```

### 4.对于超链接

**问题代码**
```html
<a href="${pageContext.request.contextPath}/servlet/RequestDemo05?userName=gacl&name=徐达沛">
点击</a>
<!--改进写法-->
<a href="${pageContext.request.contextPath}/servlet/RequestDemo05?userName=gacl&
name=<%=URLEncoder.encode("徐达沛", "UTF-8")%>">点击</a>
```

>点击超链接，数据是以get的方式传输到服务器的，解决办法就以get方式提交表单的处理方法一致。
