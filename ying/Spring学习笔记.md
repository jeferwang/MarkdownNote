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


## 	Spring框架中注入方式
1.SET 方式注入
 定义：使用SET方法形式为成员变量赋值
 语法：将需要的组件声明为成员变量，并提供set方法，在配置文件中使用property标签进行赋值
 2.构造注入
 定义：使用构造方法形式为成员变量赋值
 语法：将需要的组件声明为成员变量，并提供构造方法，在配置文件中使用constryctor-agr标签进行赋值
3.自动注入
 定义：使用bean标签 autowrite进行自动赋值
 语法：将需要的组件声明成员变量并提供set方法
autowire ；用来给组件中成员变量自动赋值 
byName: 根据名字赋值 工厂中组件名字与成员变量名一致自动赋值，找不到不赋值
byType : 根据类型赋值 根据成员变量的类型类型一致时自动赋值 不一致不赋值
<bean id="deptService" class="autodi.DeptServceImpl" autowrite="byType"> </bean>
注意：当工厂中存在类型两个一样时，byType会报错也就是说  当根据类型自动注入时，如果工厂存在多个类型一致的组件对象会报错

注入通用语法：
1.基本类型+String+日期类型注入使用value属性
2.对象|引用|组件类型使用ref属性
3.数组使用array标签 list使用list标签 set使用set map使用map properties使用props

## Spring核心思想
1.IOC（Inversion of Controll） 控制权力的反转
  控制反转：将原来手动通过new关键字创建对象的权力交出来，交给Spring，交给工厂由工厂创建对象过程
  依赖注入（Dependency Injection）:Spring框架不仅创建组件对象，还要在创建对象的同时帮助我们维护类与类|组件与组件之间依赖关系，因此                                                              在IOC基础上提出DI概念。
  
  依赖注入的语法：
  1.需要哪个组件就将哪个组件声明为成员变量并提供公开的SET方法  这个过程称之为依赖‘
  2.在配置文件中使用property标签为组件中的成员变量赋值的过程       这个过程称之为注入’

2.AOP
## 工厂创建对象
1.工厂原理：xml解析技术+反射+类中构造方法    //工厂中对象存储模型Map<String.Object> map
`PersonDAO O=(PersonDAO)Class.forName("scope.PersinDAOImpl").newInstance();`

2.工厂中对象的创建次数：
总结：默认工厂在创建对象时使用单例模式进行创建
dao service 可以是单例  servlet默认就是单例
struts2的action一定是多例

scope:作用用来决定工厂创建组件对象的次数
	singleton:默认值 单例
	protoytype:多例
	
init-method:指定组件中的初始化方法
destroy-method:指定组件中的销毁方法
	
  3.工厂的生命周期
  指的是工厂中的组件什么时候创建 什么时候销毁
  工厂启动：工厂中所有的单例bean会创建，工厂正常关闭，工厂中所有单例bean随之销毁 ------context.close()//工厂的正常的关闭
  对于工厂中的多里bean在每次使用时随之创建，spring工厂不负责多例bean的销毁