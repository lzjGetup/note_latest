`@QueueBinding` 是 RabbitMQ 的一个注解，用于声明队列与交换机之间的绑定关系。在 Spring Boot 应用中，通过 `@QueueBinding` 注解可以方便地配置队列与交换机之间的绑定关系，以便进行消息的路由和传递。以下是对 `@QueueBinding` 注解的详细介绍：

### 主要属性：

1. `value`：
    
    - **类型**：`@QueueBinding` 数组
    - **描述**：用于指定一个或多个队列与交换机之间的绑定关系。
2. `exchange`：
    
    - **类型**：`@Exchange` 注解
    - **描述**：指定要绑定的交换机，可以通过 `@Exchange` 注解声明或引用已经存在的交换机。
3. `key`：
    
    - **类型**：String
    - **描述**：指定绑定键，用于将队列绑定到交换机的特定路由键上。