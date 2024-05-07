除了 `@KafkaListener` 注解外，Spring Boot 集成 Kafka 还有一些其他常用的注解，用于配置生产者、消费者以及其他相关组件。以下是一些常用的注解：

1. `@EnableKafka`：
    
    - 用于启用 Kafka 相关功能的注解，通常添加在 Spring Boot 应用的配置类上。
2. `@KafkaListener`：
    
    - 用于声明 Kafka 消息监听器的注解，用于监听指定主题的消息。
3. `@KafkaHandler`：
    
    - 用于声明在使用 `@KafkaListener` 注解的类中处理消息的方法。该注解用于指定具体处理消息的方法，可以根据消息的类型进行方法的选择。
4. `@KafkaListenerContainerFactory`：
    
    - 用于配置 Kafka 消息监听容器的工厂类，可以自定义消息监听容器的配置。
5. `@KafkaProducer`：
    
    - 用于声明 Kafka 生产者的注解，可以将它添加到自定义的生产者类上。
6. `@KafkaTemplate`：
    
    - 用于声明 KafkaTemplate bean 的注解，用于向 Kafka 主题发送消息。
7. `@KafkaListenerErrorHandler`：
    
    - 用于声明 Kafka 消息监听器的错误处理器，可以自定义处理消息监听器中发生的异常的逻辑。
8. `@KafkaListenerConfigurer`：
    
    - 用于扩展 KafkaListener 的配置，可以在应用启动时动态地配置 KafkaListener。

这些注解提供了在 Spring Boot 应用中与 Kafka 集成时的常用配置选项，使得开发者可以方便地配置 Kafka 生产者、消费者以及消息监听器等组件。