---
layout: post 
title: "父子表 - Bootstrap"
date: 2017-08-04 14:25:35 +0800
categories: [Web]
excerpt: 基于BootstrapTable插件，实现父子表
tags:
  - Web
  - Bootstrap
  - Table
  - 前端
---

### Content

* content
{:toc}

### SRC

* onExpandRow是实现子表的关键点，detailView也是必须的。
* InitSubTable(row, $detail)则是对子表的初始化。
* 在子表中再次加入onExpandRow可以实现子表的的无限循环。

```js
//部门专用table函数
function initDepTable(url, flag) {
	$("#refreshTable").bootstrapTable({ 
		url: "./" + url + "/list",
		pagination: true, 
		pageList: [10, 15, 20, 50, 'All'],
		toolbar:"#toolbar",
		clickToSelect : true,
		showRefresh: true, 
		sidePagination: "server",
		detailView: true,
		queryParams: function(params) {
			return queryParams(params, 3);
		},  
		buttonsAlign : "right",
		onLoadError :function(){
			$('#refreshTable').bootstrapTable('removeAll');
		},
		onExpandRow:function(index, row, $detail){
			InitSubTable(row, $detail);
		}
	});  
}
```
```js
//初始化子表格
 function InitSubTable(row, $detail) {
 	//获取创建子表的位置
    var $cur_table = $detail.html('<table></table>').find('table');
    //初始化子表
    $cur_table.bootstrapTable({
        url: './department/getSub?department='+row.department,
        clickToSelect: true,
        sidePagination:'server', 
        pageSize: 100,
        columns: [{
            field: 'department',
            align:'center',
            title: '部门'
        }, {
            field: 'area',
            align: 'center',
            title: '地区'
        }, {
            field: 'upDept',
            align: 'center',
            title: '隶属部门'
        }, {
            field: 'commander',
            align: 'center',
            title: '负责人'
        }, {
            field: 'contacts',
            align: 'center',
            title: '联系人'
        },{
            field: 'tel',
            align: 'center',
            title: '电话'
        }, {
            field: 'email',
            align: 'center',
            title: '邮件'
        }, {
            field: 'recorder',
            align: 'center',
            title: '填报用户'
        }, {
            field: 'auditor',
            align: 'center',
            title: '审核用户'
        }, {
            field: 'controller',
            align: 'center',
            title: '管理用户'
        },{
        	field: 'operate',
        	align: 'center',
        	formatter: 'operationFormatterForDept',
        	event: 'operateEvents',
        	title: '操&nbsp;&nbsp;作'
        }],
    });
};
```

### 效果图

![父子表效果图](/assets/images/parentchildtable.jpg)