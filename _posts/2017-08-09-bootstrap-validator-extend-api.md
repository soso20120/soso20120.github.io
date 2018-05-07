---
layout: post 
title: "部分API和扩展校验规则 - Bootstrap"
date:  2017-08-09 20:11:24 +0800
categories: [Web]
excerpt: 获取实例，isValid()，resetForm()
tags:
  - Web
  - 前端
  - Bootstrap
  - Validator
---

### Content

* content
{:toc}

### 获取validator实例

* `$("#form").bootstrapValidator(options)`：初始化

```js
var bootstrapValidator = $("#form").data("bootstrapValidator");
```

* 通过`boostrapValidator.methodName(parameters);`调用
	* methodName:例如updateStatus、validateField等
	* parameters:方法的参数等

```js
$("#form").bootstrapValidator(methodName, parameters);

//例子
$("#fomr").bootstrapValidator("updateStatus", "birthday", "NOT_VALIDATED");
```

>均可链式调用

### isValid()

验证所有的字段是否合法(要打勾)，返回true和false。

```js
$("#button").on("click", function(){
	$("#form").data("bootstrapValidator").isValid();
});
```

### resetForm(Boolean)

重置表单中设置过校验的内容，隐藏所有错误提示和图标。

```js
$("button").on("click",function(){
	//验证不通过
	if(!$("#form").data("bootstrapValidator").isValid()){
		$("#form").data("bootstrapValidator").resetForm();
	}
});
```

### 拓展验证规则

```js
//在bootstrap.validator.js的后面添加
;(function($) {  
   //notExsit是验证的名字，default是默认信息  
    $.fn.bootstrapValidator.i18n.notExsit = 
    	$.extend( $.fn.bootstrapValidator.i18n.notExsit 
    		   || {}, { 'default': 'Please enter a valid VIN number' }); 
    $.fn.bootstrapValidator.validators.notExsit = {  
        validate: function(validator, $field, options) {  
            var value = $field.val();  
            if (value === '') {  
                return true;  
            }  
            var validateFieldStr=$(options['validateField']).html();  
            alert(validateFieldStr);  
            if(validateFieldStr==undefined){  
                return true;  
            }  
            return false;  
        }  
    };  
}(window.jQuery));  
```
