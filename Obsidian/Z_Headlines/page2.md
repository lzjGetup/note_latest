
# 分布式ID
>![[Pasted image 20240213180052.png]]

# snowflake

>![[Pasted image 20240213195245.png]]
>


# DFA

DFA（Deterministic Finite Automaton）算法在敏感词统计中可以用于快速有效地识别文本中是否包含敏感词。首先，将敏感词构建成一个DFA自动机，然后对待检测的文本进行扫描。在扫描的过程中，利用DFA自动机的状态转移特性，可以高效地判断文本中是否包含敏感词，以及敏感词的具体位置。

通过使用DFA算法，可以在较短的时间内对大量文本进行敏感词检测，因为DFA算法的时间复杂度与文本长度和敏感词数量无关，而仅与敏感词的长度相关。这使得DFA算法成为一种高效的敏感词统计工具，适用于需要实时或高吞吐量的文本过滤和监控场景。


# OCR

OCR是Optical Character Recognition的缩写，意为光学字符识别。它是一种技术，能够将印刷体或手写体的文本转换成可编辑的电子文档。通过使用OCR技术，人们可以将纸质文档、照片或扫描件中的文字转换成数字文本，以便于编辑、搜索和存档。


# tess4j

Tess4J是一个基于Java的OCR库，它提供了与Tesseract OCR引擎的集成。Tesseract是一个开源的OCR引擎，能够识别各种语言的文本。Tess4J使得在Java应用程序中使用Tesseract变得更加容易，它提供了简单的API来进行图像文本识别。这使得开发人员可以很方便地在他们的Java应用程序中实现文本识别功能。



# Mp乐观锁

==采用版本号来用于分辨每次的操作,避免产生错误读写==

>![[Pasted image 20240217114616.png]]

>![[Pasted image 20240217114525.png]]

# SCAN

Redis的SCAN命令用于迭代遍历集合中的元素。它可以用于遍历大型集合而不会阻塞服务器，因为它使用游标来逐步获取元素。SCAN命令返回一个包含元素和下一个游标的数组，可以使用这个下一个游标来进行下一次迭代。这个命令可以用于实现分批处理大型数据集，而不会对性能造成太大影响。


# Scheduled

`@EnableScheduling //开启调度任务`需要添加到启动类上面

Spring框架提供了一种方便的方式来创建定时任务。你可以使用Spring的`@Scheduled`注解来标记一个方法，以便让Spring容器知道这个方法应该定期执行。你可以指定方法执行的时间间隔或者具体的执行时间。例如，你可以使用@Scheduled(fixedRate=1000)来指定一个方法每隔一秒执行一次，或者使用`@Scheduled(cron=" 0 * * * * * ")`来指定一个方法每分钟执行一次。这种方式非常适合需要定期执行某些任务的场景，比如定时清理数据、发送邮件等。


# kafka
## 名词解释
==1)Broker==
Kafka集群包含一个或多个服务器，这种服务器被称为broker。broker端不维护数据的消费状态，提升 了性能。直接使用磁盘进行存储，线性读写，速度快:避免了数据在JVM内存和系统内存之间的复制， 减少耗性能的创建对象和垃圾回收。

==2)Producer==
负责发布消息到Kafka broker

==3)Consumer==
消息消费者，向Kafka broker读取消息的客户端，consumer从broker拉取(pull)数据并进行处理。

==4)Topic==
每条发布到Kafka集群的消息都有一个类别，这个类别被称为Topic。(物理上不同Topic的消息分开存 储，逻辑上一个Topic的消息虽然保存于一个或多个broker上但用户只需指定消息的Topic即可生产或消 费数据而不必关心数据存于何处)

==5)Partition==
Parition是物理上的概念，每个Topic包含一个或多个Partition.

==6)Consumer Group==
每个Consumer属于一个特定的Consumer Group(可为每个Consumer指定group name，若不指定 group name则属于默认的group)

==7)Topic & Partition==
- Topic在逻辑上可以被认为是一个queue，每条消费都必须指定它的Topic，可以简单理解为必须指明把 这条消息放进哪个queue里。

- 为了使得Kafka的吞吐率可以线性提高，物理上把Topic分成一个或多个 Partition，每个Partition在物理上对应一个文件夹，该文件夹下存储这个Partition的所有消息和索引文 件。

- 若创建topic1和topic2两个topic，且分别有3个和2个分区，则整个集群上会相应会生成共5个 文件夹。


## 高可用

>![[Pasted image 20240218171924.png]]


