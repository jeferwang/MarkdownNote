---
title: jquery学习笔记
tags: jquery学习笔记
grammar_cjkRuby: true
---
[TOC]
# 核心函数
  //原生入口 此function可以取到html中元素
        window.onload=function () {
           //1.通过原生的js入口函数可以拿到DOM元素
            var img = document.getElementsByTagName("img")[0];
            console.log(img);
            //2.通过原生的js入口函数可以拿到DOM的宽高
            var width = window.getComputedStyle(img).width;
            console.log(("onload", width));
        }
        
        
   //jquery入口function中可以取到html中元
        $(document).ready(function () {
            //1.通过jquery入口函数可以拿到DOM元素
            var $img = $("img");
            console.log($img)
            //2.通过jquery入口函数不可以拿到DOM元素的宽度
            var $width = $img.width();
            console.log(("ready"+$width));
        })
        //第二种写法，推荐这种写法
        $(function () {
        })
        
        
   //$():就代表调用jquery的核心函数
        //1.接受一个函数
        $(function () {
            //2.接收一个字符串
            //2.1接收一个字符选择器
            //返回一个jquery对象，对象中保存了找到的DOM元素
            var $box1 = $(".box1");
            var $box2 = $("#box2");
            //2.2接收一个字符串代码片段
            var $p = $("<p>我是段落</p>");
        //3.接收一个DOM元素
        //会被包装成一个jquery对象返回给我们
            var span = document.getElementsByTagName("span")[0];
            var $span = $(span);
        })
# jquery对象
   $(function () {
           //jquery对象是一个伪数组，伪数组就是有0到length-1属性，有length属性
           console.log($("div"));
           var attr=[0,1,2,3]
           console.log(attr);
       })
	   
# 静态方法
## map和each方法
 //数组
      var obj=[0,1,2,3,4]
      //伪数组
      var attr={0:1,1:2,2:3,length:3};

  /*  第一个参数：要遍历的数组
   第二个参数：每遍历一个元素之后执行的回调函数
   回调函数的参数：
   第一个参数:遍历到的元素
   第二个参数：遍历到的索引
   注意点：和jquery中的each静态方法一样，map静态方法也可以遍历伪数组
   */
      var res=$.map(obj,function (value,index) {
       console.log((index, index));
       return value+index;
   })

  //jquery中的each静态方法遍历数组
  /*  第一个参数：要遍历的数组
  第二个参数：每遍历一个元素之后执行的回调函数
  回调函数的参数：
  第一个参数:遍历到的索引
  第二个参数：遍历到的元素
  注意点：jquery中的each静态方法可以遍历伪数组
  */
  var res2=$.each(obj,function (index,value) {
	  console.log((index,value));
  })


/*
jquery中的each方法和Map中的静态方法的区别
 each静态方法默认返回值就是遍历谁返回谁
map静态方法默认的返回值是一个空数组
each静态方法不支持在回调函数中对遍历的函数进行处理 map静态方法可以在回调函数中通过return对遍历的数组进行处理，然后生成一个新的数组返回
*/




   //原生foreach  第一个参数：遍历到的元素，
   // 第二个参数：当前遍历的索引
   // 只能遍历数组，不能遍历伪数组
	obj.forEach(function (value,index) {
		console.log((index, index));
	})
	
## 其他静态方法
 var str=" inj  ";
     //去除空格会返回一个新的字符串
     var trim = $.trim(str);

 //真数组
 var attr=[0,1,2,3,4]
 //伪数组
 var arrlike={0:1,1:2,2:3,length:3};
 //对象
 var obj={"name":"inj","age":"33"};
 //方法
 var fn=function(){}
 //window对象
 var w = window;
 //判断传入的对象是否为window false|true
 var res = $.isWindow(w);
 //判断是否为真数组 false|true
 var res=$.isArray(obj);
 //判断是否为函数 false|true
 //注意：jQuery本质上是一个函数
 var res=$.isFunction(fn);
 
 var  btn = document.getElementsByTagName("button")[0];
       btn.Onclick=function () {
           $.holdReady(false);
           alert("btn")
       }

   //暂停入口函数的执行
   $.holdReady(true);
   $(document).ready(function () {
	   //恢复入口函数的执行
	   alert("ready")

   })
 # 内容选择器
 //empty作用：找到既没有文本内容也没有子元素的指定元素
 //parent：找到有文本内容或有子元素的指定元素
 //contains(text):包含text内容的指定元素
 //has(selector):包含子元素selector如span的指定元素
 
# 属性和属性节点
- 什么是属性
对象身上保存的变量就是属性
如何操作属性
            对象.属性名称=值
            对象.属性名称
            对象["属性名称"]=值
            对象["属性名称"]
- 什么是属性节点
<span name="666"></span>
在编写HTML代码时，在HTML标签中添加的属性就是属性节点
在浏览器中找到span这个dom元素之后展开看到的都是属性，在attributes属性中保存的所有内容都是属性节点

 - 如何操作属性节点
dom元素.setAttribute("属性名称"，"值")
var span=document.getElementsByTagName("span")[0];
span.setAttribute("name","666")
console.log(span.getAttribute("name"));
- 属性和属性节点有什么区别*/
任何对象都有属性，但是只有DOM元素有属性节
