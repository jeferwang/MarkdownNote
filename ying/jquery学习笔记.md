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
