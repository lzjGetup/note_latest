# CAP定理

CAP定理是分布式系统理论中的重要概念，它指出在一个分布式计算系统中，**一致性（Consistency）、可用性（Availability）、分区容忍性（Partition Tolerance）这三个特性不可能同时被满足。**

- 一致性（Consistency）指的是所有节点在同一时间看到的数据是一致的，即在数据写入后，所有节点都能读取到最新的数据。
- 可用性（Availability）指的是系统提供的服务必须一直可用，即使部分节点出现故障也不影响整体的可用性。
- 分区容忍性（Partition Tolerance）指的是系统在遇到网络分区故障时仍能继续运行。

CAP定理指出在分布式系统中，最多只能同时满足这三个特性中的两个，而无法同时满足全部三个。
这意味着在设计分布式系统时，需要在一致性、可用性和分区容忍性之间进行权衡取舍。


# BASE理论

>![[Pasted image 20240205182619.png]]

>![[Pasted image 20240205200955.png]]

>![[Pasted image 20240205201243.png]]


## Seata

>![[Pasted image 20240205202823.png]]

>![[Pasted image 20240205202844.png]]


### XA


>![[Pasted image 20240205204159.png]]

>![[Pasted image 20240205205826.png]]


###  AT

>![[Pasted image 20240206134847.png]]


**简述AT模式与XA模式最大的区别是什么?**
- XA模式一阶段不提交事务，锁定资源;AT模式一阶段直接提交，不锁定资源。
- XA模式依赖数据库机制实现回滚;AT模式利用数据快照实现数据回滚，
- XA模式强一致;AT模式最终一致


### AT模式写隔离

>![[Pasted image 20240206140943.png]]

非seata管理的全局事务2与事务1争抢DB锁的极端情况

>![[Pasted image 20240206140836.png]]

**AT模式的优点:**
- 一阶段完成直接提交事务，释放数据库资源，性能比较好
- 利用全局锁实现读写隔离
- 没有代码侵入，框架自动完成回滚和提交
**AT模式的缺点:**
- 两阶段之间属于软状态，属于最终一致
- 框架的快照功能会影响性能，但比XA模式要好很多

>![[Pasted image 20240206141713.png]]


### TCC模式

>![[Pasted image 20240206142728.png]]




**TCC模式的每个阶段是做什么的?**
1. Try:资源检查和预留
2. Confirm:业务执行和提交
3. Cancel:预留资源的释放
**TCC的优点是什么?**
1. 一阶段完成直接提交事务，释放数据库资源，性能好
2. 相比AT模型，无需生成快照，无需使用全局锁，性能最强
3. 不依赖数据库事务，而是依赖补偿操作，可以用于非事务型数据库
**TCC的缺点是什么?**
1. 有代码侵入，需要人为编写try、Confirm和Cancel接口，太麻烦
2. 软状态，事务是最终一致
3. 需要考虑Confirm和Cancel的失败情况，做好幂等处理



>![[Pasted image 20240206150657.png]]

>![[Pasted image 20240206151127.png]]


>![[Pasted image 20240206151321.png]]


TCC实践
[高级篇Day2-03-动手实践](https://www.bilibili.com/video/BV1LQ4y127n4/?p=149&spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=c9f01c4138ffca623361215fe6c00336)

### saga


>![[Pasted image 20240206154116.png]]

>![[Pasted image 20240206154134.png]]




