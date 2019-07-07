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

