---
title: Spring学习笔记
tags: Spring学习笔记
grammar_cjkRuby: true
---
[TOC]

# Spring框架
## Spring定义
Spring 框架是一个集众多设计模式于一身的开源的，轻量级的项目管理框架，致力于JAVAEE轻量级解决方案。
java 23种设计模式：工厂模式 代理设计模式 单例设计模式 适配器设计模式 策略设计模式等
## Spring框架核心作用
Spring 框架就是一个项目管理框架，Spring框架就是用来管理项目中组件的
  管理：负责组件对象的创建 使用 销毁
  Spring 工厂|容器
  
  注意：Spring框架一般不接管entity组件的创建
  
  ## Spring环境搭建
  1.引入依赖
  2.生成Spring框架的配置文件
  3.创建组件
  4.通过工厂管理组件

创建组件对象
bean:用来管理组件对象的创建
class:用来书写要创建组件对象的全限定名 包.类
name或者id:用来创建对象在工厂的唯一标识
<bean name= "bb"  class="day1.UserDAOimpl"></bean>
```java
//启动工厂
ApplicationContext context =new ClassPathXmlApplicationContext("day1/spring.xml")
//获取组件对象
//参数1：获取组件对象的唯一标识
UserDAO  userDAO=(UserDAO)context.getBean(“bb”);
//调用方法
userDAO.save("小明");
```
  