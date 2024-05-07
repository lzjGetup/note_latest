## @RabbitListener

`@RabbitListener` 是 Spring AMQP 中用于声明消息监听器的注解。在 `@RabbitListener` 注解中，可以包含多个属性来配置消息监听器的行为。下面是一些常用的属性及其介绍：

1. `id`: 用于指定监听器的唯一标识符。
    
2. `containerFactory`: 指定用于创建消息监听容器的 `RabbitListenerContainerFactory` bean 的名称。该容器用于管理消息监听器的生命周期和线程处理。
    
3. `queues`: 指定监听的队列名称或者 `@Queue` 注解的引用。
    
4. `bindings`: 用于指定队列与交换机之间的绑定关系。可以使用 `@QueueBinding` 注解来配置绑定关系，包括队列名称、交换机名称、交换机类型以及绑定键等信息。
    
5. `concurrency`: 指定消息监听器的并发消费者数量。可以设置为固定的数量或者使用区间值表示最小和最大并发消费者数。
    
6. `autoStartup`: 指定是否在 Spring 上下文启动时自动启动消息监听器。
    
7. `ackMode`: 指定消息确认模式，包括自动确认、手动确认和自动批量确认等。
    
8. `admin`: 指定 `RabbitAdmin` bean 的名称，用于声明队列、交换机以及绑定关系。
    
9. `exclude`: 用于排除某些监听器的配置，支持正则表达式。
    
10. `exclusive`: 指定是否为独占消费者。当设置为 `true` 时，消息监听器将独占该队列的消费。
    
11. `group`: 指定消费者组的名称，用于分组管理相同业务逻辑的多个消费者。
    
12. `priority`: 指定消息监听器的消费优先级。
    
13. `returnExceptions`: 指定是否返回异常信息。
    
14. `requeueRejected`: 指定是否在处理失败的消息时重新将其放回队列。
    
15. `defaultRequeueRejected`: 指定是否在处理失败的消息时重新将其放回队列，作为默认行为。
    
16. `durableSubscription`: 指定是否持久化订阅。
    
17. `exclusive`: 指定是否为独占订阅。
    
18. `prefetch`: 指定消息预取的数量。
    
19. `shutdownTimeout`: 指定关闭容器时的超时时间。
    
20. `concurrencyFactory`: 指定用于创建并发消费者的工厂类。
    
21. `autoDeclare`: 指定是否自动声明队列和交换机。
    
22. `adviceChain`: 指定用于监听消息处理过程的增强器链。
    
23. `phase`: 指定监听器在容器中的启动顺序。