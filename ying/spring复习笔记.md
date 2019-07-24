---
title: spring复习笔记
tags:spring
grammar_cjkRuby: true
---
[TOC]

# spring 引言
## spring定义
 spring框架是一个集众多设计模式于一身的==开源的，轻量级的项目管理框架 #F44336==。致力于JAVAEE轻量级解决方案。
 java23种设计模式：工厂设计，代理设计模式，单例设计模式，适配器设计模式，策略设计模式
 轻量级：提供一个以==简单的，统一的，高效 #F44336==的方式构造整个应用，并且可以将单层框架以最佳的组合柔和在一起建立一个连贯的体系
## spring框架的核心作用
 spring框架就是一个项目管理框架，==spring框架就是用来管理项目中组件的 #F44336==
 管理：负责组件对象的==创建 使用 销毁 #F44336==
 ==spring 工厂|容器 #F44336==
 >注意 spring框架一般不接管entity组件的创建
 # 环境搭建
 - 1.引入依赖  4.3.2版本 jdk8
 spring-core
 spring-context
 spring-beans
 spring-expression
 spring-aop
 spring-jdbc
 spring-tx
 spring-context-support
 spring-web
 
 - 2.生成spring框架配置文件
 名字：随便 spring.xml
 位置：随便src/main/resources
 
- 3.创建组件
 UserDAO UserDAOImpl
 
 4.通过工厂管理组件对象创建

``` javascript
创建组件对象
bean：用来管理组件对对象的创建 
class:  作用用来书写要创建组件对象的全限定名   包.类
name:  作用创建对象在工厂中的唯一标识

<bean name="bb" class="day1.UserDAOImpl"> <bean/>
```
5.启动工厂并在工厂获取指定组件对象

``` javascript
1.启动工厂
ApplicationContext context = new ClassPathXmlApplicationContext("day1/spring.xml");
2.获取组件对象   参数1：获取组件对象的唯一标识
	UserDAO userDAO =(UserDAO)context.getBean("bb");
3.调用方法
userDAO.save("小明");
```
# spring中核心思想
## IOC
IOC(Inversion of Controll) 控制反转 控制权力的反转

控制反转： 就是将原来手动通过new关键字创建对象的权力交出来，交给spring，交给工厂由工厂创建对象过程。

依赖注入（Dependecy Injection）:spring框架不仅要创建组件对象，还要在创建对象的同时帮助我们维护类与类，组件与组件之间依赖关系，因此在IOC基础上提出DI概念。

依赖注入语法：
	1.需要哪个组件就将哪个组件声明为成员变量并提出公开的set方法 这个过程称之为依赖
	2.在配置文件中使用property标签为组件中的成员赋值的过程 这个过程称之为注入
 # spring框架中注入方式
 ## SET方式注入
 定义：使用SET方法形式为成员变量赋值
 语法：将需要的组件声明为成员变量并提供SET方法 ，在配置文件中使用property标签进行赋值
 ## 构造注入
 定义：使用构造方法形式为成员变量赋值
 语法：将需要的组件声明为成员变量并提供构造方法在配置文件中使用constructor-agr标签进行赋值
 >注意：使用构造方法时不能自己注入自己
 ## 自动注入
 定义：使用bean标签 autowired进行自动赋值
 语法：将需要的组件声明为成员变量并提供set方法
 	
``` javascript
    byType: 根据类型
	byName: 根据名称
	
	<bean id="deptService" class="autodi.DeptServiceImpl" autowire="bytype"> <bean>
```
>	注意：根据类型自动注入时，如果工厂中存在多个类型一致的组件对象报错

 ## 注入通用语法
 1.基本类型+string+日期类型的注入使用value属性
 2.对象|引用|组件类型使用的ref属性
 3.数组使用array标签  list使用list   set使用set  map使用map  properties使用props标签