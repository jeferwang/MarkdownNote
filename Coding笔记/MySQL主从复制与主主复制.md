---
title: MySQL主从复制与主主复制
tags: MySQL
grammar_cjkRuby: true
---

最近对MySQL的高级应用挺感兴趣的，无意中看到一篇[MySQL主从复制](https://www.cnblogs.com/phpstudy2015-6/p/6485819.html)介绍的文章，仿照大牛学习了一下这个知识点，增加自己技能点的同时给简历增点色，在此对原文作者表示感谢

在数据量和访问量越来越大的情况下，单台主机已经很难满足一些企业的需求，MySQL分布式集群可以很好地解决这个问题，在MySQL集群中，比较重要的一点就是服务器之间的数据同步，本篇文章介绍的就是MySQL主从复制和主主复制的相关知识和操作

# 搭建两台测试服务器

## 安装MySQL

我的开发测试环境使用运行在Windows上的两台VMware虚拟机，由于之前已经有了一个Deepin虚拟机，所以直接拿来用，使用VMware的虚拟机克隆可以很方便的创建多个虚拟机

```shell
sudo apt update
sudo apt install mysql-server
```

## 测试是否能正常启动

分别启动两台主机，检查MySQL服务是否能正常启动

```shell
sudo 
```