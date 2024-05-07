`@Queue` 是 RabbitMQ 的一个注解，用于声明队列。在 Spring Boot 应用中，通过 `@Queue` 注解可以方便地声明 RabbitMQ 中的队列，并在需要的地方引用它。以下是对 `@Queue` 注解的详细介绍：

### 主要属性：

1. `name`：
    
    - **类型**：String
    - **描述**：指定队列的名称。如果未指定，系统将生成一个唯一的随机名称。
2. `durable`：
    
    - **类型**：boolean
    - **默认值**：true
    - **描述**：指定队列是否持久化。持久化的队列在 RabbitMQ 服务器重启后仍然存在。
3. `autoDelete`：
    
    - **类型**：boolean
    - **默认值**：false
    - **描述**：指定是否在所有消费者断开连接后自动删除队列。当最后一个消费者断开连接时，队列会自动被删除。
4. `exclusive`：
    
    - **类型**：boolean
    - **默认值**：false
    - **描述**：指定是否为独占队列。独占队列只能被声明它的连接使用，并在连接关闭时自动删除。
5. `ignoreDeclarationExceptions`：
    
    - **类型**：boolean
    - **默认值**：false
    - **描述**：指定是否忽略声明队列时的异常。如果设置为 true，在队列声明失败时不会抛出异常。
6. `arguments`：
    
    - **类型**：Map<String, Object>
    - **默认值**：空 Map
    - **描述**：指定队列的参数，可以设置一些额外的属性，如消息过期时间、队列长度限制等。