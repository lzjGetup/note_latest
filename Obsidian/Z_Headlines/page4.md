# MongoDB



>![[Pasted image 20240220121714.png]]


# xxl-job

XXL-Job是一个分布式任务调度平台，它提供了任务调度、任务执行、任务监控等功能。通过XXL-Job，用户可以方便地管理定时任务和分布式任务，并且可以实时监控任务的执行情况。这个平台可以帮助用户更好地管理和调度各种任务，提高系统的稳定性和可靠性。

### 具体使用

1. 新增执行器
>![[Pasted image 20240220204127.png]]

2. 新增任务
>![[Pasted image 20240220204256.png]]

注意以上两图的
`AppName`:执行器名称,用于配置文件

>![[Pasted image 20240220205659.png]]

`JobHandler`:任务处理器,用于注解`@XxlJob([JobHandler])`,该注解用于方法上

#### 路由策略
![[Pasted image 20240504180742.png]]





# kafka stream

  
`Kafka Stream`是一个用于构建应用程序和微服务的客户端库，其中输入和输出数据存储在Apache Kafka集群中。它提供了一种实时处理和分析数据的方式，可以创建强大的流处理应用程序。Kafka Stream允许开发人员利用Kafka的消息队列特性来构建实时数据处理应用程序，处理流式数据。这使得开发人员能够构建具有高吞吐量和容错性的实时应用程序。



# jenkins

Jenkins是一个开源的持续集成（CONTINUOUS INTEGRATION）和持续交付（Continuous delivery）工具，它可以帮助开发团队自动化软件构建、测试和部署的过程。
通过Jenkins，开发人员可以设置自动化的构建任务，监控代码的变化，并在代码提交后自动进行构建、测试和部署。


