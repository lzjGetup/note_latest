# MyBatisPlus
## 特性
>![[Pasted image 20231003192616.png]]


## 常见注解

>![[Pasted image 20240105160534.png]]


## 常用配置

>![[Pasted image 20240105161142.png]]



## 自定义Sql

>![[Pasted image 20240105170230.png]]


## 继承IService接口,使用MP方法

service接口,继承IService<实体>

```java
public interface MyUserService extends IService<MyUser> {  
}
```

service接口实现类,继承ServiceImpl<mapper接口,实体>

```java
public class MyUserServiceImpl extends ServiceImpl<MyUserMapper, MyUser> implements MyUserService  {  
}
```


## 批处理方案
>![[Pasted image 20240105193024.png]]


## 代码生成器

>![[Pasted image 20240105193831.png]]

## 静态工具类

  
MyBatis-Plus 是 MyBatis 的增强工具，在 MyBatis 的基础上进行了扩展，提供了更多便捷的操作数据库的方法。MyBatis-Plus 的静态工具类是指其中的一个工具类，它提供了一些静态方法，可以方便地进行数据库操作，比如增删改查等。这些静态方法可以直接通过类名调用，无需创建对象，使用起来非常方便。通过使用 MyBatis-Plus 的静态工具类，可以简化数据库操作的代码，提高开发效率。


## 逻辑删除

MyBatis-Plus 中的逻辑删除是指在数据库中并不真正删除数据，而是通过修改数据的状态来达到“删除”的效果。在 MyBatis-Plus 中，可以通过在实体类中添加一个标记逻辑删除的注解（@TableLogic），然后在对应的数据库表中添加一个表示逻辑删除状态的字段（比如 is_deleted），当进行删除操作时，实际上是将这个字段的值修改为已删除的状态，而不是真正地从数据库中删除数据。

```yaml
mybatis-plus:
  global-config:
    db-config:
      logic-delete-value: 1  # 逻辑已删除值（默认为 1）
      logic-not-delete-value: 0  # 逻辑未删除值（默认为 0）
```


## 枚举处理器

>![[Pasted image 20240106111813.png]]


## json处理器

>![[Pasted image 20240106112642.png]]


## 分页插件

>![[Pasted image 20240106113004.png]]


## Swagger

Swagger 是一个用于构建和描述 RESTful API 的工具，它可以通过注释来生成 API 文档。以下是 Swagger 中常用的注释：

1. `@Api`：用于对类进行说明，表示这个类是一个资源类。
2. `@ApiOperation`：用于对方法进行说明，表示一个 HTTP 请求的操作。
3. `@ApiParam`：用于对参数进行说明。
4. `@ApiModel`：用于对类进行说明，表示一个返回响应的信息。
5. `@ApiModelProperty`：用于对类的属性进行说明。
6. `@ApiImplicitParam`：用于对请求参数进行说明。
7. `@ApiImplicitParams`：用于对请求参数列表进行说明。
8. `@ApiResponse`：用于对响应进行说明。
9. `@ApiResponses`：用于对响应列表进行说明。

这些注释可以帮助开发者更好地描述 API 的信息，包括请求参数、响应信息等，使得生成的 API 文档更加清晰和易于理解。
