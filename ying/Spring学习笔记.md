---
title: Spring学习笔记
tags: Spring学习笔记
grammar_cjkRuby: true
---
[TOC]

# Spring框架
## Spring定义
Spring 框架是一个集众多设计模式于一身的开源的，轻量级的项目管理框架，致力于JAVAEE轻量级解决方案。
项目管理：spring框架负责对项目中组件的创建，销毁，使用
Spring不同于之前Struts2 mybatis 对之前项目中框架进行整合和管理
java 23种设计模式：工厂模式 代理设计模式 单例设计模式 适配器设计模式 策略设计模式等
## Spring框架核心作用
Spring 框架就是一个项目管理框架，Spring框架就是用来管理项目中组件的
  管理：负责组件对象的创建 使用 销毁
  Spring 工厂|容器
  
  注意：Spring框架一般不接管entity组件的创建
  
  ## Spring环境搭建
  1.引入依赖
  2.生成Spring框架的配置文件
  3.创建组件 如UserDAO UserDAOImpl
  4.通过工厂管理组件创建

创建组件对象
bean:用来管理组件对象的创建
class:用来书写要创建组件对象的全限定名 包.类
name或者id:用来创建对象在工厂的唯一标识

当一个组件需要组件②就把组件②设置成成员变量 并设置set方法 并在配置文件中通过property依赖注入 
```java
<bean id= "bb"  class="day1.UserDAOimpl">
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
## Spring核心思想（重点）
### 1.IOC（Inversion of Controll） 控制权力的反转
  控制反转：将原来手动通过new关键字创建对象的权力交出来，交给Spring，交给工厂由工厂创建对象过程
  依赖注入（Dependency Injection）:Spring框架不仅创建组件对象，还要在创建对象的同时帮助我们维护类与类|组件与组件之间依赖关系，因此 在IOC基础上提出DI即依赖注入概念。
  
  依赖注入的语法：
  1.需要哪个组件就将哪个组件声明为成员变量并提供公开的SET方法  这个过程称之为依赖‘
  2.在配置文件中使用property标签为组件中的成员变量赋值的过程       这个过程称之为注入’

### 2.AOP
AOP:Aspect Oriented Programming 面向切面的编程
通过为项目中某些组件在程序运行过程中动态生成代理对象，通过代理对象解决现有项目中通用问题，如事务控制，日志记录，性能统计
Target:目标对象
Advice （通知，额外，附加操作）:除了目标以外的操作都称之为通知 事务 日志 性能
PointCut(切入点);用来告诉项目中哪些类中哪些方法需要加入通知
Aspect(切面)：Advice(通知)+PointCut(切入点)

AOP的编程思路:目标对象
1.引入AOP的相关jar
2.开发通知类
MethodBeforeAdvice 前置通知
AfterReturningAdvice 后置通知 
ThroesAdvice 异常通知
MethodInterceptor 环绕通知
3.工厂管理通知
bean id-="" class="xxxx.xxxadvice"
4.配置切面
a.配置切入点
<aop:pointCut...>
b.配置
5.启动工厂测试即可
### AOP编程之环绕通知
1.引入jar
2.开发环绕通知
类 implements MethodInterceptor{

}
3.管理通知类
4.管理切面

## 	Spring框架中注入方式
1.SET 方式注入（重点）
 定义：使用类中SET方法形式为成员变量赋值
 语法：将需要的组件声明为成员变量，并提供set方法，在配置文件中使用property标签进行赋值
 2.构造注入
 定义：使用类中构造方法形式为类中成员变量赋值
 语法：将需要的组件声明为成员变量，并提供构造方法，在配置文件中使用constructor-arg标签进行赋值
 注意：构造注入不能自己注入自己
3.自动注入
 定义：使用bean标签 autowrite进行自动赋值，根据类型或者名称自动为类中成员变量赋值
 语法：将需要的组件声明成员变量并提供set方法，在配置文件中自动赋值的bean标签是哪个使用autowried属性赋值
autowire ；用来给组件中成员变量自动赋值 
byName: 根据名字赋值 工厂中组件名字与成员变量名一致自动赋值，找不到不赋值
byType : 根据类型赋值 根据成员变量的类型类型一致时自动赋值 不一致不赋值
<bean id="deptService" class="autodi.DeptServceImpl" autowrite="byType"> </bean>
注意：当工厂中存在类型两个一样时，byType会报错也就是说  当根据类型自动注入时，如果工厂存在多个类型一致的组件对象会报错

注入通用语法：
1.基本类型+String+日期类型注入使用value属性
2.对象|引用|组件类型使用ref属性
3.数组使用array标签 list使用list标签 set使用set map使用map properties使用props

## 工厂创建对象（重点）
1.工厂原理：xml解析技术+反射+类中构造方法    //工厂中对象存储模型Map<String.Object> map
`PersonDAO O=(PersonDAO)Class.forName("scope.PersinDAOImpl").newInstance();`

2.工厂中对象的创建次数：（重点）
总结：默认工厂在创建对象时使用单例模式进行创建，可以通过bean标签中的scrop属性修改为多例
<bean id="xx" class="xxx" scope="singleton|prototype">  </bean>
dao service 可以是单例  servlet默认就是单例
struts2的action一定是多例

scope:作用用来决定工厂创建组件对象的次数
	singleton:默认值 单例
	protoytype:多例
	
init-method:指定组件中的初始化方法
destroy-method:指定组件中的销毁方法
	
  3.工厂的生命周期（重点）
  指的是工厂中的组件什么时候创建 什么时候销毁
  单例bean:工厂启动,工厂中所有的单例bean会创建，工厂正常关闭，工厂中所有单例bean随之销毁 ------context.close()//工厂的正常的关闭
  多例bean:在每次使用工程时才会进行创建，即对于工厂中的多例bean在每次使用时随之创建，spring工厂不负责多例bean的销毁，交由虚拟机jvm
# 代理引言
- 1.现有业务层存在问题
问题：在现有业务层开发中控制事务的代码存在大量冗余
- 2.什么是代理
代理指的是java的一种设计模式
代理对象保证原始功能不变，从而进一步增加额外功能
- 3.能不能使用代理对象解决现有业务层问题
解决方案：
a:将控制事务代理交给代理执行
b.业务层只专注于业务逻辑对象
- 4.静态代理对象开发
为现有业务层组件手动开发一个代理对象的过程，称之为静态代理对象
代理对象开发原则：代理对象和业务逻辑实现相同接口，代理对象中一定依赖于业务逻辑对象（目标对象）
静态代理对象存在的问题：手动为每一个业务层组件开发一个代理对象====》静态代理对象的创建
1.类文件过多，不利于我们维护
2.增加工作量
- 5.解决静态代理存在的问题====》动态代理
动态代理：在程序运行过程中动态为项目中某些对象创建代理对象，然后再通过创建动态代理对象执行附加操作
Object o=proxy.newProxyInstance(当前线程类加载，创建代理对象的接口类型，new InvocationHanlder方法(){
public Object invoke(Object proxy,Method m,	Object[] args){
//附加操作
Object resault=m.invoke(new UserviceImpl(),args)
//附加操作
return result;
}
})
proxy.xxxx;
- 6.AOP 面向切面的编写
通知Advice （通知，额外功能，附加操作）:除了目标以外的操作都称之为通知    事务 日志 性能
PointCut(切入点);用来告诉项目中哪些类中哪些方法需要加入通知
Aspect(切面)：Advice(前置|后置|环绕|异常通知)+PointCut(切入点)
- 7.AOP编程思路
a.引入AOP的相关jar
b.开发通知类
MethodBeforeAdvice 前置通知
AfterReturningAdvice 后置通知 
ThroesAdvice 异常通知
MethodInterceptor 环绕通知
c.配置通知，工厂管理通知
bean id-="" class="xxxx.xxxadvice"
d.配置切面
<aop:config>
<aop:pointcut>
<aop:advosor>
</aop:config>
e.启动工厂从工厂获取指定对象 注意：被切入点切中组件获取的是代理对象而不是原始对象
- 8.前置通知。。。。
- 9.切入点表达式
方法级别切入点表达式：execution(返回值类型 包.类名.方法名（参数类型）)
类别级别切入点表达式： within(包.类名)
- 10.多个切面的执行顺序（重点）
a.多个aop切面的执行顺序默认是配置顺序
b.在标签<aop:advisor order="">  order为 int 整数  数字越小优先执行 一旦执行order属性配置顺序失效。 order 值相同 配置顺序优先
- 11.spring框架中有几种创建代理对象的方式 分别是什么 有什么区别(重点)
2种 
JDK：提供Proxy  根据接口生成代理对象  默认使用jdk中的Proxy
Spring ：提供CGLIB 根据实现类生成代理对象
修改spring框架默认生成代理对象为CGLIB
<aop:config proxy-traget-class="false(Proxy)|true(CGLIB)">


## 代理对象
代理作用：起到了传话作用，增强业务逻辑对象的功能，中断原始的业务逻辑
如何开发一个代理对象：
1.代理对象和业务逻辑对象（目标对象）实现相同的接口
2.代理对象中依赖于真正的业务逻辑对象（目标对象）

### 静态代理 
静态代理：为现有业务层对象手动的开发一个代理对象过程，静态代理对象
问题：为每一个业务层组件手动开发一个代理对象不仅会增加我们的工作量还会使我们程序维护更加困难
### 动态代理
动态代理：指的是在程序运行过程中由JVM自动根据指定对象去动态生成代理对象
目标对象（Target）：被代理的对象称之为目标对象 也就是真正的业务逻辑对象
创建代理对象：
```java
//Proxy:用来创建代理对象  
//返回值：为当前创建的代理对象
//参数1：类加载对象
//参数2：创建代理对象的目标对象的接口的类型
//参数3：当使用创建代理对象调用代理对象中方法时会优先执行InvocationHandler类中的invoke方法
ClassLoader classLoader=Thread.currentThread().getContextClassLoader();
Class[] classes=new Class[]{UserService.class};
Object o = Proxy.newProxyInstance(classLoader.classes,new InvocationHandler{

//参数1：Proxy当前代理对象‘
//参数2：Method 当前代理对象调用的方法对象
//参数3：agrs:当前代理对象调用的方法传递的参数
@override
public Obiect invoke(参数1.2.3）{

参数1：调用哪个类中当前方法
参数2：调用方法时的参数
method.invoke(Obiect,Object...);
method.invoke(userService,args);
return invoke;
}
]);
```
## 复杂对象
1.复杂对象
不同直接new关键字创建的组件
java.sql.connection 连接对象
java.util.Calendar  抽象类

2.复杂对象通过工厂创建的编程

CalendarFactoryBean implements FactoryBean<Calendar>(){
getObject              用来指定复杂对象的创建方法
getObjectType      创建对象类型
isSingleton            是否是单例，否为多例


# Spring + mybatis==>SM整合
1.引入依赖
Spring  mybatis  Mysql

2.SM整合====》如何整合？
Spring 项目管理框架  主要用来负责项目中组件对象的创建 使用 销毁
Mybatis 持久层框架    主要用来简化jdbc对数据库访问操作

> 整合思路：Spring整合mybatis框架实际上将mybatis框架中核心对象交给spring框架管理

3.Mybatis中核心对象有哪些
1.DAO对象
2.sqlSession对象
3.sqlSessionFactory 对象 核心对象 最先创建
直接依赖于mybatis-config.xml文件

- 一定依赖于数据源对象
- 一定依赖于mapper文件注册

