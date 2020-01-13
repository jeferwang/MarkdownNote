---
title:  Kafka
tags: Kafka
grammar_cjkRuby: true
---


[TOC]

# 术语解释
## broker
KafKa集群包含一个或多个服务器，服务器节点成为broker
## Topic
每条发布到KafKa集群的消息都有一个类别 这个类别被称为Topic
## Partition
topic中的数据分割为一个或多个Partition每个Topic至少有一个partition.每个partition中的数据使用多个segment文件存储，partition中数据是有序的，不同partititon间的数据丢失了数据的顺序，如果topic有多个partition,消费数据时就不能保证数据的顺序。在需要严格保证消息的消费顺序的场景下。需要将partition数据设为1
## Producer
生产者即数据的发布者，该角色将消息发布到Kafka的topic中。