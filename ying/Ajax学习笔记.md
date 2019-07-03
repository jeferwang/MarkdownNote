---
title: Ajax学习笔记
tags: Ajax学习笔记
grammar_cjkRuby: true
---
[TOC]

# Ajax
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
```javascript
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
2.Ajax的post请求编程思路

a.创建xhr
```javascript
var xhr;
if(XMLhttpResquest){
	xhr=new XMLhttpRequest();
}else{
	xhr=new ActiveXObject("Microsoft.XMLHTTP");
}
```
b.发送请求并传递参数
```javascript
xhr.open("POST","URL");
xhr.setRequestHeader("content-type","application/x-www-form-urlencoded");
xhr.send("name=z&&psw=123456");
```
c.处理响应 并刷新页面局部
```javascript
	if(xhr.readState==4 &&xhr.status==200){
			xhr.responseText;//获取后台字符串request.getWriter.print(“字符串”)
	}
```
3.ajax的数据传递机制之JSON
 例子：异步展示一个人的信息
 编程思路：
 a.按钮绑定click事件
 b获取指定id
 c.发送ajax请求
 1）创建xhr
 2)发送请求传递id
 3)处理响应，更新页面布局
 
 ```java
 //编程步骤
 $(function(){
 	//1.绑定单击事件
	$("#btn").click(function(){
		var id=21;
		//ajax的get请求思路
	})
 })
 ```