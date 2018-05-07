---
layout: post 
title: "How to use Jekyll"
date: 2017-07-11 11:11:11 +0800
categories: [Blog]
excerpt: 这是一个学习Jekyll及搭建blog的经验过程。不断更新。
tags:
  - jekyll
---

### Content

* content
{:toc}

### 0 为什么要使用jekyll

jekyll是一个静态网页生成器，它可以把markdown格式写的文章转为html网页这样的东西。

### 1 Directory Structure - jekyll导航目录

	.
	├── _config.yml       [配置文件，blog基本信息]
	├── _data            *[数据文件，当格式为.yml、.yaml、.json、.csv会被自动解析为site.data]			
	|   └── members.yml  *[可直接在content中用site.data.members引用]
	├── _drafts           [草稿，即不会被发布，使用jekyll serve或kjekyll build --drafts预览]
	|
	├── _includes         [layouts和posts的零件]
	|   ├── head.html     [包含meta标签]
	|   ├── header.html   [导航栏]
	|   ├── banner.html   [横幅]
	|   |
	|   ├── about.html    [主页关于]
	|   ├── blogs.html    [主页进入blog]
	|   ├── projects.html [主页projects]
	|   |
	|   ├── post-list-pagination.html  [分页，但是好像并没有生效]
	|   ├── post-pagination.html       [文章中可直接跳转上一篇和下一篇post]
	|   ├── share.html    [文章下的分享按钮]
	|   ├── comments.html [评论插件]
	|   ├── footer.html   [页脚图标及版权]
	|   └── analytics.html 
	|
	├── _layouts          [包装posts的模板，用{content}在网页注入content]
	|   ├── default.html  [最基本的页面head、header、banner、content、comments、footer、analytics]
	|   ├── post.html     [default，post的header与body(content、post-pagination、share、comments)]
	|   ├── post-list.html[放在default中，tab页面及post-list-pagination]
	|   └── tags.html     [放在default中，content及share]
	|
	├── _posts            [即文章，命名必须遵守y-m-d-title.MARKUP，链接可自定义]
	|   └──               [每篇post的layout即post]
	├── _sass            *[样式]
	|   └──
	├── _site             [默认的生成站点所在地]
	├── .jekyll-metadata *[帮助jekyll追踪最后一次生成站点未被修改的文件]
	├── index.html        [使用default模板，包含head]
	|	
	|   以下是本主题所包含的自定义文件及文件夹
	├── assets							
	|   ├── _sass
	|   |   ├── vendor
	|   |   |   ├── font-awesome
	|   |   | 	|   ├── _font-awesome.scss [包含该文件下除_extra所有文件]
	|   |   | 	|   ├── _animated.scss
	|   |   | 	|   ├── _bordered-pulled.scss
	|   |   | 	|   ├── _core.scss
	|   |   | 	|   ├── _extras.scss *
	|   |   | 	|   ├── _fixed-width.scss
	|   |   | 	|   ├── _icons.scss
	|   |   | 	|   ├── _larger.scss
	|   |   | 	|   ├── _list.scss
	|   |   | 	|   ├── _mixins.scss
	|   |   | 	|   ├── _path.scss
	|   |   | 	|   ├── _rotated-flipped.scss
	|   |   | 	|   ├── _stacked.scss
	|   |   | 	|   └── _variables.scss	
	|   |   |   └── font.scss
	|   |   ├── _base.link.scss  
	|   |   ├── _base.scss
	|   |   ├── _base.text.scss
	|   |   ├── _components.img.scss *
	|   |   ├── _components.nav.scss
	|   |   ├── _components.tag.scss
	|   |   ├── _layout.scss
	|   |   ├── _syntax-highlighting.scss
	|   |   ├── _tools.mixins.scss
	|   |   ├── _settings.color.scss
	|   |   ├── _settings.fonts.scss
	|   |   └── _settings.device.scss
	|   ├── css
	|   |   └── main.cscc    [引入各部分，除了components.img及font-awesome下其他]
	|   ├── fonts            [字体文件]
	|   ├── images           [图片]
	|   └── js
	|       ├── jPages.js
	|       ├── script.js
	|       ├── svg-animation.js
	|       └── 插件的js
	|
	├── meta
	|   ├── tags.md	
	|   └── posts.md
	├── 404.html             [错误网页提示]
	├── feed.xml
	├── CNAME                [外站域名]
	├── LICENSE.md           [本主题的授权]
	└── README.md            [本主题的使用须知]

<br>
### 2 \_config\.yml

<br>
💙 Configuration Settings

* Global Configuration - 全局设定
 
&emsp;&emsp;&emsp;不是很看得懂

* Build Command Options - 关于生成站点的设置

&emsp;&emsp;&emsp;也看不懂

* Serve Command Options - 服务与发布设置

&emsp;&emsp;&emsp;1.`port`：本地服务端口<br>

&emsp;&emsp;&emsp;2.`host`：本地服务主机名<br>

&emsp;&emsp;&emsp;3.`baseurl`：发布url<br>

&emsp;&emsp;&emsp;4.`？detach`：从终端分发服务

💙 Custom WEBrick Headers

&emsp;&emsp;不懂

💙 Specifying a Jekyll environment at build time

&emsp;&emsp;不懂

🧡 Front Matter defaults - 页面设置值

&emsp;可以实现自定义应用区域的默认值:

	defaults:
	 -
	   scope:
	   	path:""           [空表明所有]
	   	type:"pages"
	   values"
	    layout:"my-site"
	 -
	   scope:
	   	path:"projects"
	   	type:"pages"
	   values"
	    layout:"project"
	    author:"Mr.Hyde"

&emsp;当然，也可以在post或page中写新的front matter。

* Predefined Gobal Variables - 预定义的全局变量

&emsp;&emsp;`layout`:表明使用的模板，null表示不用任何模板，但是会被defaults覆盖

&emsp;&emsp;`permalink`:永久url，会覆盖掉默认的

&emsp;&emsp;`published`：设为false时不会生成

>只用于Posts
>
>`date`：此处能覆盖名字中的日期，格式YYYY-MM-DD HH:MM:SS +/-TTTT
>
>`categories`：分类，可以设置一个或更多
>
>`tags`：标签，也设置多个
>
> --- 下的内容被识别为content

<br>

🧡 Default Configuration

	# Where things are
	source:          .
	destination:     ./_site
	collections_dir: .
	plugins_dir:     _plugins
	layouts_dir:     _layouts
	data_dir:        _data
	includes_dir:    _includes
	collections:
	  posts:
	  output:   true

	# Handling Reading
	safe:                 false
	include:              [".htaccess"]
	exclude:              ["Gemfile", "Gemfile.lock", "node_modules", "vendor/bundle/", "vendor/cache/", "vendor/gems/", "vendor/ruby/"]
	keep_files:           [".git", ".svn"]
	encoding:             "utf-8"
	markdown_ext:         "markdown,mkdown,mkdn,mkd,md"
	strict_front_matter: false

	# Filtering Content
	show_drafts: null
	limit_posts: 0
	future:      false
	unpublished: false

	# Plugins
	whitelist: []
	plugins:   []

	# Conversion
	markdown:    kramdown
	highlighter: rouge
	lsi:         false
	excerpt_separator: "\n\n"
	incremental: false

	# Serving
	detach:  false
	port:    4000
	host:    127.0.0.1
	baseurl: "" # does not include hostname
	show_dir_listing: false

	# Outputting
	permalink:     date
	paginate_path: /page:num
	timezone:      null
	quiet:    false
	verbose:  false
	defaults: []
	liquid:
	  error_mode: warn

	# Markdown Processors
	rdiscount:
	  extensions: []
	redcarpet:
	  extensions: []
	kramdown:
	  auto_ids:       true
	  entity_output:  as_char
	  toc_levels:     1..6
	  smart_quotes:   lsquo,rsquo,ldquo,rdquo
	  input:          GFM
	  hard_wrap:      false
	  footnote_nr:    1



<br>
<br>
<hr>

###### 学习好难
	
	调整标题阴影
	tag字体太大
	.gitignore有看不懂的
	<!-- * content{:toc} -->
	page-list-paginaiton文件
	如何调用about。blog。projects


<br>
<hr>
附上搭博客的指导：
<br>
1.<a href="http://www.jianshu.com/p/8f843034c7ec">“授人以渔”的教你搭建个人独立博客</a>
<br>
2.<a href="https://jekyllrb.com/docs/">Jekyll说明文档<i class="fa fa-fw fa-hand-o-left"></i></a>