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

当一个组件需要组件②就把组件②设置成成员变量 并设置set方法 并在配置文件中通过property依赖注入 
```java
<bean name= "bb"  class="day1.UserDAOimpl">
//为类中成员变量赋值的过程称之为注入（Injection）

property:用来为类中声明的成员变量赋值
name:用来指定类中赋值的成员变量名
ref:用来指定赋值对象在工厂中的唯一标识
<property name="cityDAO" ref="aa"></property>
</bean>

//启动工厂
ApplicationContext context =new ClassPathXmlApplicationContext("day1/spring.xml")
//获取组件对象
//参数1：获取组件对象的唯一标识
UserDAO  userDAO=(UserDAO)context.getBean(“bb”);
//调用方法
userDAO.save("小明");

```
## Spring核心思想
1.IOC（Inversion of Controll） 控制权力的反转
  控制反转：将原来手动通过new关键字创建对象的权力交出来，交给Spring，交给工厂由工厂创建对象过程
  依赖注入（Dependency Injection）:Spring框架不仅创建组件对象，还要在创建对象的同时帮助我们维护类与类|组件与组件之间依赖关系，因此                                                              在IOC基础上提出DI概念。
  
  依赖注入的语法：
  1.需要哪个组件就将哪个组件声明为成员变量并提供公开的SET方法  这个过程称之为依赖‘
  2.在配置文件中使用property标签为组件中的成员变量赋值的过程       这个过程称之为注入’

2.AOP
  