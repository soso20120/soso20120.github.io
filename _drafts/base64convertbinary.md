---
layout: post 
title: "文件base64转二进制 - JS"
date: 2017-07-24 08:24:25 +0800
categories: [Web]
excerpt: 对JS，基于FormData，如何实现base64转二进制文件
tags:
  - Web
  - JS
  - 前端
---

未实验

```js
function dataURItoBlob(dataURI) {
	//去掉url的头，并转换为byte
    var byteString = atob(dataURI.split(',')[1]);
    //mimeString可能得到'image/png'
    var mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];
    var ab = new ArrayBuffer(byteString.length);
    var ia = new Uint8Array(ab);
    for (var i = 0; i < byteString.length; i++) {
        ia[i] = byteString.charCodeAt(i);
    }
    return new Blob([ab], {type: mimeString});
}
```
