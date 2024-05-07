`@KafkaListener` 注解是 Spring Kafka 提供的用于声明 Kafka 消息监听器的注解，用于监听指定主题的消息。`@KafkaListener` 注解具有多个属性，用于配置消息监听器的行为。以下是 `@KafkaListener` 注解的常用属性：

1. `id`：
    
    - **类型**：String
    - **描述**：指定监听器的唯一标识符。
2. `topics`：
    
    - **类型**：String[] 或 String
    - **描述**：指定要监听的 Kafka 主题名称，可以是一个字符串数组或者单个字符串。如果监听多个主题，则可以使用字符串数组。
3. `topicPattern`：
    
    - **类型**：String
    - **描述**：指定要监听的 Kafka 主题的模式。可以使用正则表达式来匹配多个主题。
4. `groupId`：
    
    - **类型**：String
    - **描述**：指定消费者组的标识符。如果不指定，则使用默认的消费者组。
5. `clientIdPrefix`：
    
    - **类型**：String
    - **描述**：指定客户端ID的前缀。可以用于在生成的客户端ID中添加自定义前缀。
6. `containerFactory`：
    
    - **类型**：String
    - **描述**：指定用于创建消息监听容器的 `KafkaListenerContainerFactory` bean 的名称。该容器用于管理消息监听器的生命周期和线程处理。
7. `concurrency`：
    
    - **类型**：int
    - **描述**：指定消息监听器的并发消费者数量。可以设置为固定的数量或者使用区间值表示最小和最大并发消费者数。
8. `autoStartup`：
    
    - **类型**：boolean
    - **描述**：指定是否在 Spring 上下文启动时自动启动消息监听器。
9. `topicPartitions`：
    
    - **类型**：TopicPartition[]
    - **描述**：指定要监听的具体主题分区。可以指定主题和分区的组合来进行消息监听。
10. `containerGroup`：
    

- **类型**：String
- **描述**：指定消息监听容器组的标识符。可以用于将多个消息监听器组织成一个组。

11. `errorHandler`：

- **类型**：String
- **描述**：指定消息监听器的错误处理器 bean 的名称。用于处理消息监听器中发生的异常。

12. `beanRef`：

- **类型**：String
- **描述**：指定消息监听器 bean 的名称。用于将消息监听器声明为 Spring bean，以便在其他地方引用。

13. `factory`：

- **类型**：String
- **描述**：指定用于创建 Kafka 消息监听器 bean 的工厂类的名称。可以自定义消息监听器的创建过程。

14. `condition`：

- **类型**：String
- **描述**：指定消息监听器的条件表达式。只有满足条件的消息才会被监听。

15. `splitIterables`：

- **类型**：boolean
- **描述**：指定是否将可迭代的消息拆分为单个消息进行处理。

16. `ackMode`：

- **类型**：ContainerAckMode
- **描述**：指定消息确认模式，包括自动确认、手动确认和自动批量确认等。

17. `useDefaultContainerFactory`：

- **类型**：boolean
- **描述**：指定是否使用默认的消息监听容器工厂。如果设置为 true，则忽略 `containerFactory` 属性，使用默认的工厂类。

18. `pollTimeout`：

- **类型**：long
- **描述**：指定从 Kafka 主题中拉取消息的超时时间。

19. `clientId`：

- **类型**：String
- **描述**：指定客户端ID。用于唯一标识消费者客户端。

20. `properties`：

- **类型**：String[]
- **描述**：指定 Kafka 消费者配置属性。可以通过数组形式指定多个配置属性。