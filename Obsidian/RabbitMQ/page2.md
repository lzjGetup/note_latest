# 消息可靠性

>![[Pasted image 20240131233839.png]]

>![[Pasted image 20240131234629.png]]



>![[Pasted image 20240201113049.png]]



>![[Pasted image 20240201113327.png]]



>![[Pasted image 20240201113703.png]]



>![[Pasted image 20240201114758.png]]

## lazyQueue

>![[Pasted image 20240201131636.png]]

## 消费者确认

>![[Pasted image 20240201132446.png]]


>![[Pasted image 20240201132553.png]]


>![[Pasted image 20240201133324.png]]

>![[Pasted image 20240201133800.png]]


>![[Pasted image 20240201133932.png]]

在配置类顶部标注
`@ConditionalOnProperty(XXX)`
即可实现当配置生效时才进行spring装配


# 业务幂等性

业务幂等性是指无论对一个业务操作进行多少次重复操作，其结果都是一致的。换句话说，对于同一笔业务，无论进行多少次操作，最终的结果都是一样的。这种特性通常在分布式系统中非常重要，因为在分布式系统中，由于网络等原因，可能会导致消息重复发送或者操作重复执行，而业务幂等性可以确保最终的结果是一致的。

==MQ解决方案==

>![[Pasted image 20240201140507.png]]

#### 小结
>![[Pasted image 20240201142633.png]]
## 死信交换机

>![[Pasted image 20240201143754.png]]

## 发送延迟消息

1. MQ在插件目录中安装延迟插件
**安装插件命令**
```c
docker exec -it mq rabbitmq-plugins enable rabbitmq_delayed_message_exchange
```
其中mq为容器名字

2. java使用延迟消息

>![[Pasted image 20240201155131.png]]











