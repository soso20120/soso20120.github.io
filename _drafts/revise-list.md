---
layout: post
title: Sample post
feature-img: "assets/img/sample_feature_img.png"
excerpt: 摘要
url:
date: 
categories： 
tags: [test, sample]
---

需要改进的清单
1. about.html 介绍
2. rss
3. readme
4. 样式
5. 主页每个博文占面积太大，改样式
6. disqus评论系统
7. 头像
8. 网页图标
9. 加分类
10. 考虑多平台适应性
11. 暂时去掉了摘要
12. 文章中的tag一定要调整
13. 考虑加个注释字体

其中全局根结点有
```
site _config.yml 中配置的信息
page 页面的配置信息
content 模板中,用于引入子节点的内容
paginator 分页信息
```
site 下的变量
```
site.time 运行 jekyll 的时间
site.pages 所有页面
site.posts 所有文章
site.related_posts 类似的10篇文章,默认最新的10篇文章,指定lsi为相似的文章
site.static_files 没有被 jekyll 处理的文章,有属性 path, modified_time 和 extname.
site.html_pages 所有的 html 页面
site.collections 新功能,没使用过
site.data _data 目录下的数据
site.documents 所有 collections 里面的文档
site.categories 所有的 categorie
site.tags 所有的 tag
site.[CONFIGURATION_DATA] 自定义变量
```
page 下的变量
```
page.content 页面的内容
page.title 标题
page.excerpt 摘要
page.url 链接
page.date 时间
page.id 唯一标示
page.categories 分类
page.tags 标签
page.path 源代码位置
page.next 下一篇文章
page.previous 上一篇文章
```
paginator 下的变量
```
paginator.per_page 每一页的数量
paginator.posts 这一页的数量
paginator.total_posts 所有文章的数量
paginator.total_pages 总的页数
paginator.page 当前页数
paginator.previous_page 上一页的页数
paginator.previous_page_path 上一页的路径
paginator.next_page 下一页的页数
paginator.next_page_path 下一页的路径
```

github page的问题不要用百度搜：垃圾百度被hacker用来攻击github ，百度就被屏蔽了，使用搜狗搜jekyll问题,gitbub上专门解决各类问题的社区存在，记得换浏览器就行了；要不然找不到的；

[jekyll基本结构](http://ju.outofmemory.cn/entry/141586)

# 关于模板嵌套
主页：index引用layout-home

home-->layout-default
page-->layout-default
post-->layout-default{
	post_nav
	disqus
}

tags-->layout-tags-->layout-page
search-->layout-page

default{
	head -->css及js等引用
		--> main.scss-->type-theme.scss-->all
	header -->icons
	{{content}}
	footer
}

assets{
	image-->only for image in posts
	js
	css
}