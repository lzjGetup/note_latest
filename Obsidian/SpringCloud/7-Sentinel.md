# 微服务雪崩问题

>![[Pasted image 20240204163417.png]]


# 安装Sentinel
>![[Pasted image 20240204164518.png]]

>![[Pasted image 20240204165138.png]]


用于查看控制台其他配置
[Sentinel_wiki](https://github.com/alibaba/Sentinel/wiki/%E6%8E%A7%E5%88%B6%E5%8F%B0)


# 簇点链路

>![[Pasted image 20240205133050.png]]

>![[Pasted image 20240205133634.png]]

==新增流控规则==

>![[Pasted image 20240205133945.png]]

>![[Pasted image 20240205134005.png]]

# 流控

### 模式

>![[Pasted image 20240205134931.png]]


- 默认为直接,即对当前资源限流;
- 关联模式一般用于两个有竞争关系的资源,一个优先级高,一个优先级低,对优先级低的设置关联限流;
- 链路模式则是对请求的来源进行限流



==注意==:Sentinel 仅仅默认对controller的资源进行监控.倘若需要监控service的资源,则需要添加注解,以及修改context配置(避免整合);

>![[Pasted image 20240205140409.png]]


## 效果

>![[Pasted image 20240205140844.png]]


### WarmUP
>![[Pasted image 20240205141326.png]]


### 排队等待

排队等待可以通过配置 Sentinel 的规则来实现，开发者可以设置最大的排队等待时间和队列长度，以及超出队列长度后的拒绝策略。
这样可以根据系统的实际情况来灵活地控制流量，保护系统的稳定性和可靠性。



### 热点限流

>![[Pasted image 20240205142634.png]]


# 隔离和降级

>![[Pasted image 20240205150428.png]]


>![[Pasted image 20240205151119.png]]


### 实现过程

>![[Pasted image 20240205151339.png]]

>![[Pasted image 20240205151406.png]]


#### 线程隔离

>![[Pasted image 20240205153516.png]]

##### 线程隔离(舱壁模式)
>![[Pasted image 20240205153623.png]]

## 熔断降级

>![[Pasted image 20240205154211.png]]
>

>![[Pasted image 20240205154423.png]]


>![[Pasted image 20240205155038.png]]

## 授权规则

>![[Pasted image 20240205155907.png]]

>![[Pasted image 20240205155941.png]]


>![[Pasted image 20240205160113.png]]

## 异常处理返回结果

>![[Pasted image 20240205161603.png]]
>



## 规则持久化

Sentinel的各种规则默认保存在内存中,因此需要将规则持久化,以便长期使用.此部分开源社区版不支持.需要修改源码.













