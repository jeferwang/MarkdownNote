---
title: Ajax学习笔记
tags: Ajax学习笔记
grammar_cjkRuby: true
---
[TOC]

# 一.Ajax
## Ajax的核心对象

  XMLHttpRequest对象是一个javaScrip对象，存在浏览器差异，简称xhr对象

## Ajax核心编程思路

ajax异步请求 特点：请求之后页面不动 响应回来刷新页面局部

1.Ajax的GET方式编程思路
① 绑定用户名失去焦点事件

a.获取用户输入的用户名
b.创建xhr对象，屏蔽浏览器差异  IE  |  WebKit chrome 火狐 欧朋 
 ``` java 
	  var xhr;
	  winddow.XMLHttpRrequest    true为webKit    false为IE
	  
	  if(window.XMLHttpRequest){
	  		xhr=new XMLHttpRequest();
	  }else{
	  		xhr=new ActiveXObject("Microsoft.XMLHTTP");
	  }
 ```
c.发送请求，并传递参数
``` java 
			xhr.open("GET","url?name=z&p=123");
			xhr.send();//发送请求
 ```
d.处理响应并更新页面局部
```javascript?linenums
	xhr.onreadystatechange=function(){
		xhr.readyState  
		0 xhr未初始化
		1 xhr 已经初始化
		2 xhr 发送请求
		3 xhr 请求已经开始响应
		**4 xhr 请求已经完整响应**
	}
	//xhr.ststus 400 404 500 495 200
	if(xhr.readState==4 &&xhr.status==200){
			xhr.responseText;//获取后台字符串request.getWriter.print(“字符串”)
	}
```

