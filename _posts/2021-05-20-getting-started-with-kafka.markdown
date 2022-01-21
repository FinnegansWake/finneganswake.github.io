---
layout:     post
title:      "从头了解Kafka"
subtitle:   "一份Kafka的简明教程"
date:       "2021-05-20"
author:     "Boreas Ma"
header-img: "img/post-bg-kafka.png"
tags:
    - 后端
    - 消息队列
    - 流处理平台
comments: true
---
> **Apache Kafka** is a framework implementation of a software bus using stream-processing. It is an open-source software platform developed by the Apache Software Foundation written in Scala and Java. The project aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds. -- WikiPedia [Apache Kafka](https://en.wikipedia.org/wiki/Apache_Kafka)

[Kafka](https://kafka.apache.org/)是Apache软件基金会发布的一个开源流处理平台，今天的内容是一个Kafka的简明教程。

# 0x0 Kafka使用的一些基本概念
Kafka使用了一些基本的的概念来作为运行的一个抽象：[events](https://kafka.apache.org/documentation/#messages)以及[topics](https://kafka.apache.org/documentation/#intro_topics)。根据Kafka文档中的解释，events就如同日常生活中的支付的事务、手机地址信息的更新，这样的信息集合。events本组织并储存在topics中，topics就如同文件系统中的文件夹，而events就像是文件夹中的文件。

# 0x1 获取Kafka
使用Kafka之前首先要获取Kafka的release包。[这是Kafka官方的下载链接](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.8.0/kafka_2.13-2.8.0.tgz)，点击链接后就会进入Kafka的的下载地址：![经典的Kafka下载页面](/img/in-post/post-getting-started-with-kafka/kafka-download.png)这个页面也提供了使用`PGP`签名技术验证文件完整性的方法，对于普通用户来说，这一步是可选的，所以不再赘述。\
下载软件包，然后解压之，就可以得到一个可运行的Kafka环境：
```
$ tar -xzf kafka_2.13-2.8.0.tgz
```
切换到Kafka的目录，开始准备接下来的使用：
```
$ cd kafka_2.13-2.8.0
```

# 0x2 运行Kafka环境
*注意：运行Kafka环境之前需要确保本地已经安装了Java 8+* \
\
运行以下指令来启用与Kafka运行相关的服务：
```
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```
由于Kafka是一个运行在Zookeeper上的分布式流处理平台，因此需要运行Zookeeper服务来是Kafka正常运转。
运行这条命令后，Zookeeper服务开始运行：
![Zookeeper开始运行](/img/in-post/post-getting-started-with-kafka/zookeeper-start.png) \
接下来打开一个新的终端来开启Kafka的服务：
``` 
bin/kafka-server-start.sh config/server.properties
```
运行后的结果如下：
![Kafka开始运行](/img/in-post/post-getting-started-with-kafka/kafka-start.png)
一个基本的Kafka环境正在运行中，下面让我们尝试一下具体的使用
# 0x3 创建Topic来存储你的事件
Kafka使用topic来存储events，打开新的终端，运行如下指令来创建一个名称为`quickstart-events`的topic
```
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```
其中，`--create --topic`参数的作用是创建一个制定名称的topic，`--bootstrap-server`参数的作用是直接连接到给定的broker。
在Kafka运行的图中我们可以看到，broker的运行地址是localhost:9092，其中9092也正是Kafka运行的端口号，这是一个本地环回地址，因此我们在`--bootstrap-server`的后面填上Kafka的broker的运行地址。\
目前版本的Kafka支持不添加旧版的`--zookeeper`参数就可运行系统，本教程选择采用新版本Kafka的使用方法，也就是不添加`--zookeeper`参数。

运行该指令之后的结果如图：
![创建topic](/img/in-post/post-getting-started-with-kafka/create-topic.png)
可以看到，Kafka会提示创建了`quickstart-events`这一topic。










