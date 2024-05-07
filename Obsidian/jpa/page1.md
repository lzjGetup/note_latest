## 启动

### 依赖

```java
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>  
<dependency>  
    <groupId>com.mysql</groupId>  
    <artifactId>mysql-connector-j</artifactId>  
</dependency>
```

### 配置
```yml
spring:  
  datasource:  
    url: jdbc:mysql://127.0.0.1:3306/jpa?useUnicode=true&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC  
    username: root  
    password: 123456  
    driver-class-name: com.mysql.cj.jdbc.Driver  
  
  jpa:  
    generate-ddl: on  
    hibernate:  
      ddl-auto: update
```


### 使用
```java
public interface UserRepository extends JpaRepository<User,Integer> {  
}
```
`<T,ID>`,第一部分表示实体类,即pojo;第二部分表示主键id的类型




#### auto-ddl
以下是常见的`ddl-auto`选项：
1. **validate**：
    - 当应用程序启动时，JPA提供者会验证数据库表的结构与实体类的映射是否匹配，但不会对数据库表进行任何更改。
    - 如果表结构与实体类的映射不匹配，则会抛出异常。
2. **update**：
    - 当应用程序启动时，JPA提供者会根据实体类的定义更新数据库表的结构，但不会删除已存在的数据。
    - 它会尽可能地保留现有的数据库表数据，并尝试根据实体类的定义修改表结构。
3. **create**：
    - 当应用程序启动时，JPA提供者会根据实体类的定义创建数据库表结构。
    - 如果表已经存在，则会删除并重新创建。
4. **create-drop**：
    - 类似于`create`选项，但是当应用程序关闭时，JPA提供者会删除数据库表结构。
    - 这对于测试和开发环境很有用，但不适合生产环境。
5. **none**：
    - JPA提供者不会执行任何数据库表结构的自动操作。
    - 你将完全负责管理数据库表的创建、更新和删除。


####  GenerationType

在JPA（Java Persistence API）中，主键生成策略是指在向数据库插入新记录时如何为实体对象生成主键值。JPA定义了几种主键生成策略，常见的有以下几种：

1. **GenerationType.IDENTITY**：
    - 使用数据库自增长（auto-increment）的方式生成主键。
    - 适用于支持自增长主键的数据库，如MySQL、PostgreSQL等。
2. **GenerationType.SEQUENCE**：
    - 使用数据库序列（sequence）生成主键。
    - 需要在数据库中创建一个序列，然后在实体类中指定使用该序列。
    - 适用于不支持自增长主键但支持序列的数据库，如Oracle等。
3. **GenerationType.TABLE**：
    - 使用数据库中的一个特殊表来存储生成的主键值。
    - 需要在数据库中创建一个用于存储主键值的表，然后在实体类中指定使用该表。
    - 每次生成主键时，都会向这个特殊表中查询并更新主键值。
    - 这种方式相对较慢，一般不推荐使用，除非没有其他选择。
4. **GenerationType.AUTO**：
    - 让JPA自动选择合适的主键生成策略，根据数据库类型进行选择。
    - 在大多数情况下，JPA会根据数据库的支持情况自动选择IDENTITY或SEQUENCE。


  
在Java Persistence API (JPA) 中，有一些常用的注解用于实现对象关系映射 (ORM)。以下是其中一些常见的注解：

1. `@Entity`: 标识实体类，表示这个类将映射到数据库中的表。
    
2. `@Table`: 用于指定实体类与数据库表的映射关系，可以指定表名、schema等信息。
    
3. `@Id`: 标识实体类的主键字段。
    
4. `@GeneratedValue`: 标识主键的生成策略，常与@Id一起使用，用于指定主键的自动生成方式，如自增、UUID等。
    
5. `@Column`: 用于指定实体属性与数据库表列的映射关系，可以指定列名、长度、是否可空等信息。
    
6. `@OneToMany`: 用于表示一对多的关联关系，通常用于实体类之间的关联。
    
7. `@ManyToOne`: 用于表示多对一的关联关系，通常用于实体类之间的关联。
    
8. `@JoinColumn`: 用于指定关联关系中的外键列的映射信息。
    
9. `@NamedQuery` / `@NamedQueries`: 用于定义命名查询，可以在实体类中定义一些常用的查询语句，方便重用。
    
10. `@Transient`: 用于指定某个属性不需要持久化到数据库中，即不与表中的列对应。


### Cascade

- ALL:所有操作都进行关联操作
- PERSIST:插入操作时才进行关联操作
- REMOVE:删除操作时才进行关联操作
- MERGE:修改操作时才进行关联操作


## Method

#### 固定参数
```java
@Query("select u from User u where u.userName='zhangsan'")  
List<User> findAllByUserName();
```

#### 占位传参

```java
@Query("update User set userName=?2 where id=?1")  
@Modifying  
@Transactional  
Integer updateUserNameById(Integer id,String username);
```

#### 集合遍历
```java
@Query(value = "select * from user where id in :ids", nativeQuery = true)  
List<User> getUserByIdIs(@Param("ids") List<Integer> ids);
```