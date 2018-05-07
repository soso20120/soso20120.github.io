---
layout: post 
title: "文件上传的实现"
date: 2017-07-21 08:14:05 +0800
categories: [Web]
excerpt: 利用FormData实现表单中文字和文件同时异步上传，后台则利用SpringMVC中的MultipartFile接收。以及使用FileReader可以实现更多前端功能
tags:
  - Web
  - SpringMVC
  - 文件上传
  - JAVA
  - 前端
  - 后台
---

# Content

* content
{:toc}

# file - HTML5

* `capture`表示可以捕获到系统默认的设备。

&emsp;&emsp;&emsp;比如：camera-照相机；camcorder-摄像机；microphone-录音。

* `accept`表示直接打开系统文件目录。

```html
	<input type="file" accept="image/*" capture="camera">
```

* `multiple`表示可以支持多选。

```html
	<input type="file" id="avatar" name="avatar" multiple>
```

<br>

---
# FomrData

### 1.what's FormData

&emsp;XMLHttpRequest Level 2添加了一个新的接口FormData，能组装请求的键/值对。比起普通的ajax，使用FormData的最大优点就是我们可以**异步上传表单文字和二进制文件**.

### 2.创建

&emsp;FormData对象的字段类型可以是`Blob` `File` `String`。如果它的字段类型不是Blob也不是File，则会被转换成字符串类型。

&emsp;需要注意的是，数字也会被转换成字符串，后台对应用字符串类型接受。

>一个 Blob对象表示一个不可变的, 原始数据的类似文件对象。Blob表示的数据不一定是一个JavaScript原生格式。File接口基于Blob，继承 blob功能并将其扩展为支持用户系统上的文件。你可以通过Blob()构造函数创建一个Blob对象。<br>
>var blob = new Blob([content], { type: "text/xml"});  //content是个变量

```js
	//创建空的对象
	var formData = new FormData();
	//创建form的FormData对象，表单中指定的method会被应用。
	var formData = new FormData(form元素);
	//通过getFormData()方法创建
	var formobj =  document.getElementById("form");
	var formdata = formobj.getFormData()；
```

### 3.方法

* **添加新值**

```js
	formData.append(name,value);
	formData.append(name,value,filename);
	formData.append('file', $('#file')[0].files[0], 'chris.jpg');
	formData.append("myfile", myBlob, "filename.txt");
```

* **设定新值**

&emsp;如何不存在，会直接在末尾加上该键值对；否则进行修改。
```js
	formData.set(name, value);
	formData.set(name, value, filename);
```

* **删除**

```js
	formData.delete(name);
```

* **取值**

&emsp;返回给定键的值，只返回value。
```js
	formData.get(name);  //只返回第一个
	formData.getAll(name);  //返回所有值，如["Justin", "Chris"]
```

* **检查是否有该值**

&emsp;检查是否包含给定键，返回true或false。
```js
	formData.has(name);
```

### 4.兼容性

Feature | Chrome | Firfox(Gecko) | Internet Explorer | Opera | Safari
----|----|----|----|----|----
Basic Support | 7+ | 4.0(2.0) | 10+ | 12+ | 5+
append with filename | (Yes) | 22.0(22.0) | ? | ? | ?

### 5.API参考

[FormData API](https://developer.mozilla.org/en-US/docs/Web/API/FormData/FormData)<i class="fa fa-fw fa-hand-o-left"></i>

<br>

---
# FileReader

&emsp;HTML5定义了FileReader作为文件API的重要成员用于读取文件，根据W3C的定义，FileReader接口提供了读取文件的方法和包含读取结果的事件模型。

&emsp;FileReader对象允许Web应用程序异步读取存储在用户计算机上的文件（或原始数据缓冲区）的内容，使用 File 或 Blob 对象指定要读取的文件或数据。

### 1.检测浏览器对FileReader的支持

```js
if(window.FileReader){
	//支持
}else{
	//不支持
}
```

&emsp;通过getElementById获取input file节点，判断浏览器的兼容性，对于不支持FileReader接口的浏览器将给出一个提示并禁用input，否则监听input的change事件。

```js
if(typeof FileReader==='undefined'){
	result.innerHTML = "抱歉，你的浏览器不支持 FileReader";
	input.setAttribute('disabled','disabled');
}else{
	input.addEventListener('change',readFile,false);
}
```

### 2.调用方法

&emsp;无论读取成功或失败，方法并不会返回读取结果，这一结果存储在`result`属性中。

&emsp;文件一旦开始读取，无论成功或失败，实例的result属性都会被填充。读取失败时，result的值为null。

方法名|参数|描述
abort|none|中断读取
readAsBinaryString|file|将文件读取为二进制码，后端可以通过这段字符串存储文件
readAsDataURL|file|将文件读取为 DataURL，该方法将文件读取为一段以**data:**开头的字符串，Data URL是一种**将小文件直接嵌入文档**的方案。这里的小文件通常是指**图像与html**等格式的文件。
readAsText|file, [encoding]|将文件读取为文本，默认值为UTF-8

### 2.处理事件

事件|描述
onabort|中断时触发
onerror|出错时触发
onload|文件读取成功完成时触发
onloadend|读取完成触发，无论成功或失败
onloadstart|读取开始时触发
onprogress|读取中

### 3.Array中File对象的属性

> `name`：文件名称，只读字符串。只包含文件名称，不包含任何路径信息<br>
> `size`：文件大小，使用bytes描述，是一个只读的64位整数<br>
> `type`：文件的MIME type，只读字符串，当类型不能确定时为""

### 4.一些功能示例

###### 成功读取文件的时候，抓取这个值。

```js
filereader.onload = function() {
    this.result;
};
```

###### 预览图片

&emsp;表单中**`onchange="showPreview(this)"`**

```js
function showPreview(source) {
	var file = source.files[0];
	if(window.FileReader) {
		var fr = new FileReader();
		fr.onloadend = function(e) {
			document.getElementById("img").src = e.target.result;
		};
		fr.readAsDataURL(file);
	}
}
```

###### 显示进度条

&emsp;使用HTML5中的`progress`

```html
<form>
    <fieldset>
        <legend>分度读取文件：</legend>
        <input type="file" id="File" />
        <input type="button" value="中断" id="Abort" />
        <p>
            <label>读取进度：</label><progress id="Progress" value="0" max="100"></progress>
        </p>
        <p id="Status"></p>
    </fieldset>
</form>
```
```js
var h = {
    init: function() {
        var me = this;
        document.getElementById('File').onchange = me.fileHandler;
        document.getElementById('Abort').onclick = me.abortHandler;
        me.status = document.getElementById('Status');
        me.progress = document.getElementById('Progress');
        me.percent = document.getElementById('Percent');
        me.loaded = 0;
        //每次读取1M
        me.step = 1024 * 1024;
        me.times = 0;
    },
    fileHandler: function(e) {
        var me = h;
        var file = me.file = this.files[0];
        var reader = me.reader = new FileReader();
        me.total = file.size;
        reader.onloadstart = me.onLoadStart;
        reader.onprogress = me.onProgress;
        reader.onabort = me.onAbort;
        reader.onerror = me.onerror;
        reader.onload = me.onLoad;
        reader.onloadend = me.onLoadEnd;
        //读取第一块
        me.readBlob(file, 0);
    },
    onLoadStart: function() {
        var me = h;
    },
    onProgress: function(e) {
        var me = h;  
        me.loaded += e.loaded;
        //更新进度条
        me.progress.value = (me.loaded / me.total) * 100;
    },
    onAbort: function() {
        var me = h;
    },
    onError: function() {
        var me = h;  
    },
    onLoad: function() {
        var me = h;
        if(me.loaded < me.total) {
            me.readBlob(me.loaded);
        } else {
            me.loaded = me.total;
        }
    },
    onLoadEnd: function() {
        var me = h;
    },
    readBlob: function(start) {
        var me = h;
        var blob,
            file = me.file;
        me.times += 1;
        if(file.webkitSlice) {
            blob = file.webkitSlice(start, start + me.step + 1);
        } else if(file.mozSlice) {
            blob = file.mozSlice(start, start + me.step + 1);
        }
        me.reader.readAsText(blob);
    },
    abortHandler: function() {
        var me = h;
        if(me.reader) {
            me.reader.abort();
        }
    }
};
h.init();
```

###### 判断文件类型

&emsp;`\w`代表任意字符

```js
//即检测image/后面的字符
if(! /image\/\w+/.test(file.type)){
    alert("请确保文件为图像类型");
    return false;
}
```


<br>

---

# File类 - Java

* `new Flie(路径或者文件名)`：仅仅定义一个指向它的指针
* `createNewFile()`：创建新文件，当文件存在时返回false
* `mkdir()`：创建目录
* `mkdirs()`：创建多级目录
* `delete()`：删除文件，当文件不存在时返回false
* `deleteOnExit()`：程序退出时，自动删除文件。一般用于对程序创建的临时文件进行操作。
* `exists()`：文件是否存在
* `isDirectory()`：是否为文件夹
* `isFile()`：是否为文件
* `getName()`：获取文件名
* `getParent()`：获取文件父目录
* `getPath()`：获取文件路径
* `getAbsolutePath()`：获取文件绝对路径
* `lastModified()`：获得文件最后一次被修改的时间
* `length()`：获取文件大小
* `renameTo()`：文件剪切，将文件f1剪切然后粘贴到f2（相当于右键f1->剪切->粘贴->f2所在目录）
* `listRoots()`：获取系统盘符
* `list()`：获取该目录下的所有文件名，包括隐藏文件和文件夹（调用list()方法时，必须先封装一个目录，且必须存在的目录。）
* `listFiles()`：列出目录下文件名，不包括文件夹

<br>

---
# MultipartFile - SpringMVC

### 1.配置文件

* `defaultEncoding`：请求的编码格式，默认为iso-8859-1
* `maxUploadSize`：是上传文件的大小，单位为字节
* `uploadTempDir`：为上传文件的临时路径

```xml
<!-- 配置MultipartResolver 用于文件上传 使用spring的CommosMultipartResolver -->  
    <beans:bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver"  
        p:defaultEncoding="UTF-8"  
        p:maxUploadSize="5400000"
        p:uploadTempDir="fileUpload/temp">  
    </beans:bean>  
```

### 2.常用方法

* `String getContentType()`：获取文件MIME类型
* `InputStream getInputStream()`：读去文件流
* `String getName()`：获取表单中文件组件的名字
* `String getOriginalFilename()`：获取上传文件的原名
* `long getSize()`：获取文件的字节大小，单位byte
* `boolean isEmpty()`：是否为空
* `void transferTo(File dest)`：保存到一个目标文件中。

<br>

---
# Example

### 1.JSP代码

&emsp;注意`<form>`中enctype，`<input>`中type="file"，`onchange`实现了上传后直接展示缩略图的功能，不通过后台。

&emsp;可参考上传按钮样式。

&emsp;提交按钮`button`若采用submit，可能会导致页面刷新，onclick实现了异步提交表单。
```html
<form class="form-horizontal" id="updateAvatorForm" method="post" enctype ="multipart/form-data">
	<div class="row">
	<!--照片输入框-->
		<div class="col-lg-6 col-md-6 col-sm-12">
			<div class="form-group">
				<div class="visible-sm-inline col-sm-1"></div>
					<div class="col-lg-3 col-md-3 col-sm-2 text-right">
						<label class="control-label tittle">照片</label>
					</div>
				<div class="col-lg-8 col-md-8 col-sm-8 padding-right-none">
					<span class="btn btn-default btn-file">上传头像<span class="glyphicon glyphicon-picture" aria-hidden="true"></span>
					<input type="file" name="updatePhoto" onchange="preview()" />
				</div>
			</div>
		</div>
	</div>
	<div class="row">
		<div class="col-lg-6 col-md-6 col-sm-12">
			<div class="form-group">
				<div class="visible-sm-inline col-sm-1"></div>
				<div class="col-lg-3 col-md-3 col-sm-2 text-right"></div>
				<div class="col-lg-8 col-md-8 col-sm-8 padding-right-none">
     				<img src="" class="img-responsive img-thumbnail hide" width="100" height="100" id="thumbnail" alt="头像缩略图">
				</div>
			</div>
		</div>
	</div>
	<div class="row" id="buttonGroup">
		<div class="col-lg-5 col-lg-offset-6 col-md-5 col-md-offset-6 col-sm-5 col-sm-offset-6 text-right">
			<button type="button" class="btn btn-warning" data-dismiss="modal">返回</button>
			<button type="button" class="btn btn-primary" onclick="updateAvator()">确认上传</button>
		</div>
	</div>
</form>
```

###### 表单展示效果
![表单-上传文件](/assets/images/form_picture.jpg)

### 2.JS代码 - FormData异步上传

**为什么是$("#updateAvatorForm")[0]**
>&emsp;jQuery是一个伪数组对象，本身是对象，能表现出来数组的特点: 有length属性，能够用下标取值。<br>
>&emsp;所以jQuery得到的是个HTMLElement的集合基础上的封装后的对象。<br>
>&emsp;而new FormData的参数需要一个HTMLElement类型的数据。

**JQuery的一些技巧**
>`$("form[0]")`取`<form>`中第一个
>`$("*[name=form1]")`匹配所有name为form1的元素

```javascript
function updateAvator(){ 
	var formData = new FormData($("#updateAvatorForm")[0]);
	formData.append('id',$("#modalAvator").data('id'));
	$.ajax({
		type : "post",
		url : "./user/updateAvator",
		data : formData,
		dataType: "json",
		cache : false,  //禁止浏览器对该URL（以及对应的HTTP方法）的缓存
		async : false,  
		contentType : false,  //因为content-type默认值为application/x-www-form-urlencoded
		processData : false,  //jQuery会将data对象转换为字符串来发送HTTP请求，默认上面的方法 
		success : function(data) {
			shuitu.modal.alert('上传头像成功！');
			$("#modalAvator").modal('hide');
			$("#refreshTable").bootstrapTable('refresh');
		},
  		error: function (data) {  
  	 		shuitu.modal.alert(data.message);
       	}  
	});
}
```

**FormData请求头**

![FormData请求头](/assets/images/ajaxuploadpicture.jpg)

### 3.JS代码 - FileReader预览图片

**获取文件列表**
>input中有一个DOM属性files，包含所选的文件列表Array<br>
>$('input[name="updatePhoto"]')[0].files<br>
>$('input[name="updatePhoto"]').get(0).files<br>
>$('input[name="updatePhoto"]').prop('files')

```js
function preview() {
	var files = $('input[name="updatePhoto"]').prop('files');
   	var reader = new FileReader();
   	reader.readAsDataURL(files[0], "UTF-8");
   	reader.onload = function () {
   		var dataURL = reader.result;
       	var img = document.getElementById("thumbnail");
       	img.src = dataURL;
       	var $img = $(img);
       	$img.removeClass("hide");
   	};
}
```

**FileReader请求头**

![FileReader请求头](/assets/images/previewImg.jpg)

>每个字段由一段boundary string来分隔，浏览器保证该boundary string不与内容重复，因而multipart/form-data能够成功编码二进制数据。

### 4.后台代码
```java
@Controller
@RequestMapping(path="user", produces = { "application/json" })
public class UserController extends BasicController{
//只截取了上传图片的内容
@ResponseBody
@RequestMapping(value = "/updateAvator", method = RequestMethod.POST)
public Result updateAvator(
		HttpServletRequest request,
		String id,  //获取文本内容id
		//获取图片，设为false也可以实现不传图片的情况，此时url中为null
		@RequestParam(value="updatePhoto",required=false)MultipartFile photo) {
	//返回一些信息，自定义的类
	Result result = new Result();
	String url = null;
	//输出pathRoot:D:\workspace\.metadata\.plugins\org.exlipse.wst.server.core\tmp0\wtpwebapps\bulletin
	String pathRoot = request.getSession().getServletContext().getRealPath("");
	//若是request.getSession().getServletContext().getRealPath("/");
	//输出pathRoot:D:\workspace\.metadata\.plugins\org.exlipse.wst.server.core\tmp0\wtpwebapps\bulletin\
	String path = "\\resources\\File";
	//输出path:\resources\File
	File f = new File(pathRoot + path);
	if (!f.exists()) {
		f.mkdirs();
	}
	//非常重要，当未传照片时，先判断photo!=null，否则photo.isEmpty()会报错
	if (photo != null && !photo.isEmpty()) {
		String fileName = photo.getOriginalFilename();
		url = path + "\\" + fileName;
		try {
			File avator = new File(pathRoot + url);
			if (!avator.exists()) {
				avator.createNewFile();
			}
			photo.transferTo(avator);
		} catch (Exception e) {
			e.printStackTrace();
			result.setMessage("文件上传失败，请重试！");
		}
	}
	//这部分为写入url至user的操作
	try {
		int idInt = Integer.valueOf(id);
		User user = userService.getUserById(idInt);
		user.setPhoto('.'+url);
		userService.updateUser(user);
	} catch (Exception ex) {
		result.setMessage("添加用户信息失败, 请重新操作");
		result.setStatus(STATUS_FAILURE);
		return result;
	}
	result.setMessage("添加用户信息成功!");
	result.setStatus(STATUS_SUCCESS);
	return result;
}
}
```
