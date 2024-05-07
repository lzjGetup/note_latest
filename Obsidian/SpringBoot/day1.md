# SpringBoot


# IDEA创建程序

>![[Pasted image 20240101185828.png]]




## 1.快速入门
>直接创建控制器类,加上标签即可

![[Pasted image 20231002092319.png]]

## 2.打包
==对于前端开发人员需要boot后端服务器进行测试,这是我们可以使用Maven生命周期的package命令打包,打包好的文件在target目录下.==

==前端人员拿到jar包后,可以直接在文件管理器中,进入cmd,输入`java -jar 文件名`,即可使用==

==另外,对于不同运行环境,可以使用命令`java -jar 文件名 -- spring.profiles.active=环境名`,去改变当前环境==

**SpringBoot 程序优点恰巧就是针对 Spring 的缺点
==自动配置==这个是用来解决 Spring 程序配置繁琐的问题
==起步依赖==这个是用来解决 Spring 程序依赖设置繁琐的问题
==辅助功能==（内置服务器...)我们在启动 SpringBoot 程序时既没有使用本地的 tomcat 也没有使用 tomcat 插件，而是使用 SpringBoot 内置的服务器。**



## 3.更换服务器(jetty)
==采用排除依赖可以排除boot给我们提供的tomcat服务器==

>![[Pasted image 20231003134718.png]]

## 4.更换端口
```java
//yaml格式配置文件(.yml),注意80前方空格不可少
server:
	port: 80
```

## 5.配置文件
*配置文件有三种格式,{.properties   .yml   .yaml},三者的加载优先级递减*

==配置文件读取数据==


>![[Pasted image 20231003141835.png]]

==简化版本==
```java
//自动加载所有配置变量
@Autowired
private Environment env;
//调用方法获取
env.getProperty("变量名")
```

==配置文件优先级==
>![[Pasted image 20231003160046.png]]

**其中classpath指的是开发IDE中的路径,file指的是打包好的文件夹中**
## 6. 封装数据源到对象
```java
//外部封装
@Component  
@ConfigurationProperties(prefix = "配置文件名")  
public class stu {  
    private int id;  
    private String name;  
    private String age;  
}

//使用
@Autowired
private stu s1;
```

## 7.多环境开发
```java
spring:  
  profiles:  
    active: test  
---  
#开发  
spring:  
  profiles: dev  
server:  
  port: 80  
---  
#测试  
spring:  
  profiles: test  
server:  
  port: 81  
---
```
**在active中可以切换**


## SpringBoot整合MyBatis
==在IDEA原生项目中,只需要先编写数据库连接信息(yml文件),写上控制类,在Dao数据层上添加`@Mapper` 注释即可==
*想要修改数据源的,需要导入(druid)坐标,然后在yml文件中Spring.datasource中type属性中说明即可*


## WebMvcConfigurer接口


在Spring Web MVC中，WebMvcConfigurer接口可以重写以下方法：

1. **addResourceHandlers**: 该方法用于添加静态资源的处理器，可以指定静态资源的访问路径和存放路径。
    
2. **configureMessageConverters**: 该方法用于配置消息转换器，可以添加自定义的消息转换器，例如将JSON转换为Java对象或将Java对象转换为JSON。
    
3. **extendMessageConverters**: 该方法用于扩展消息转换器，可以修改或替换默认的消息转换器。
    
4. **configureContentNegotiation**: 该方法用于配置内容协商策略，可以设置请求的媒体类型和对应的处理方式。
    
5. **addFormatters**: 该方法用于添加格式化器和解析器，可以自定义数据的格式化和解析方式，例如日期格式化等。
    
6. **addInterceptors**: 该方法用于添加拦截器，可以注册自定义的拦截器来拦截请求并进行处理。
    
7. **addCorsMappings**: 该方法用于配置跨域资源共享（CORS）规则，可以设置允许跨域请求的规则。


## 注释

`@ConditionalOnClass`注解是Spring Framework中的一个条件注解，它的作用是在类路径中存在指定的类时才会生效。

通常情况下，@ConditionalOnClass注解用于配置类，用来控制某个配置类是否生效，从而根据类路径中的情况来动态地决定是否加载某些配置。这样可以根据不同的类路径情况来实现更灵活的配置管理，使得应用程序在不同环境下能够更好地适配和扩展。



**下面这些注解在自定义starter是可能会用到。**

- @Conditional：按照一定的条件进行判断，满足条件给容器注册bean
- @ConditionalOnMissingBean：给定的在bean不存在时,则实例化当前Bean
- @ConditionalOnProperty：配置文件中满足定义的属性则创建bean，否则不创建
- @ConditionalOnBean：给定的在bean存在时,则实例化当前Bean
- @ConditionalOnClass： 当给定的类名在类路径上存在，则实例化当前Bean
- @ConditionalOnMissingClass ：当给定的类名在类路径上不存在，则实例化当前Bean

  

