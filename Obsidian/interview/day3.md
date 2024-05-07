## Spring是什么?
轻量级的开源的J2EE框架。它是一个容器框架，用来装javabean，中间层框架(万能胶)可以起一个连接作用，
比如说把Struts和hibernate粘合在一起运用，可以让我们的企业开发更快、更简洁Spring是一个轻量级的控制反转(loc)和面向切面(AOP)的容器框架
- 从大小与开销两方面而言Spring都是轻量级的。

- 通过控制反转(IOC)的技术达到松耦合的目的

- 提供了面向切面(AOP)编程的丰富支持，允许通过分离应用的业务逻辑与系统级服务进行内聚性的开发

- 包含并管理应用对象(Bean)的配置和生命周期，这个意义上是一个容器。将简单的组件配置、组合成为复杂的应用，这个意义上是一个框架。


## 对AOP的理解

AOP:将程序中的交叉业务逻辑(比如安全，日志，事务等)，封装成一个切面，然后注入到目标对象(具体业务逻辑)中去。
AOP可以对某个对象或某些对象的功能进行增强，比如对象中的方法进行增强，可以在执行某个方法之前额外的做一些事情，在某个方法执行之后额外的做一些事情


## 对IOC的理解

没有引入IOC容器之前，对象A依赖于对象B，那么对象A在初始化或者运行到某一点的时候，自己必须主动去创建对象B或者使用已经创建的对象B。无论是创建还是使用对象B，控制权都在自己手上。

引入IOC容器之后，对象A与对象B之间失去了直接联系，当对象A运行到需要对象B的时候，IOC容器会主动创建一个对象B注入到对象A需要的地方。


通过前后的对比，不难看出来:对象A获得依赖对象B的过程,由主动行为变为了被动行为，控制权颠倒过来了，这就是“控制反转“这个名称的由来。


全部对象的控制权全部上缴给“第三方"IOC容器，所以，IOC容器成了整个系统的关键核心，"它起到了-种类似“粘合剂”的作用，把系统中的所有对象粘合在一起发挥作用，如果没有这个"粘合剂"，对象与对象之间会彼此失去联系，这就是有人把IOC容器比喻成“粘合剂“的由来。
**依赖注入:**
"获得依赖对象的过程被反转了"。控制被反转之后，获得依赖对象的过程由自身管理变为了由IOC容器主动注入。
依赖注入是实现IOC的方法，就是由IOC容器在运行期间，动态地将某种依赖关系注入到对象之中。


## BeanFactory和Applicationcontext有什么区别?

![[Pasted image 20240426212135.png]]

![[Pasted image 20240426212350.png]]


## Spring Bean的生命周期

![[Pasted image 20240426212704.png]]

## 解释下Spring支持的几种bean的作用域。

- singleton: 默认，每个容器中只有一个bean的实例，单例的模式由BeanFactory自身来维护。该对象的生命周期是与SpringlOC容器一致的(但在第一次被注入时才会创建)。
- prototype: 为每一个bean请求提供一个实例。在每次注入时都会创建一个新的对象
- request:  bean被定义为在每个HTTP请求中创建一个单例对象，也就是说在单个请求中都会复用这一个单例对象。
- session:  与request范围类似，确保每个session中有一个bean的实例，在session到期后，bean会随之失效。
- application:  bean被定义为在Servletcontext的生命周期中复用一个单例对象。
- websocket:  bean被定义为在websocket的生命周期中复用一个单例对象

## Spring框架中的单例Bean是线程安全的么?


Spring中的Bean默认是单例模式的，框架并没有对bean进行多线程的封装处理。
如果Bean是有状态的 那就需要开发人员自己来进行线程安全的保证:
最简单的办法就是改变bean的作用域 把"singleton"改为"protopyte'这样每次请求Bean就相当于是 new Bean() 这样就可以保证线程的安全了。

- 有状态就是有数据存储功能
- 无状态就是不会保存数据
- controller、service和dao层本身并不是线程安全的，只是如果只是调用里面的方法，而且多线程调用一个实例的方法，会在内存中复制变量，这是自己的线程的工作内存，是安全的。

Dao会操作数据库Connection，Connection是带有状态的，比如说数据库事务，Spring的事务管理器使用Threadlocal为不同线程维护了一套独立的connection副本，保证线程之间不会互相影响(Spring 是如何保证事务获取同一个Connection的)

不要在bean中声明任何有状态的实例变量或类变量，如果必须如此，那么就使用ThreadLocal把变量变为线程私有的，如果bean的实例变量或类变量需要在多个线程之间共享，那么就只能使用synchronized、lock、CAS等这些实现线程同步的方法了。


## Spring框架中使用了哪些设计模式
![[Pasted image 20240427181654.png]]


![[Pasted image 20240427181717.png]]


![[Pasted image 20240427181737.png]]

![[Pasted image 20240427181842.png]]


![[Pasted image 20240427181904.png]]

## Spring事务实现方式原理以及事务隔离级别
![[Pasted image 20240427183130.png]]


spring事务隔离级别就是数据库的隔离级别:外加一个默认级别
- read uncommitted(读未提交)
- read committed(读已提交)
- repeatable read (可重复读)
- serializable(可串行化)

数据库的配置隔离级别是Read commited,而spring配置的隔离级别是Repeatable Read，请问这时隔离级别是以哪一个为准?
以spring配置的为准，如果spring设置的隔离级别数据库不支持，效果取决于数据库


## Spring事务传播机制
![[Pasted image 20240427184434.png]]


## Spring事务什么时候会失效

![[Pasted image 20240427184934.png]]


## 自动装配有哪些方式?

 spring 配置文件中 `<bean>` 节点的 autowire 参数可以控制 bean 自动装配的方式

- default: 默认的方式和 "no" 方式一样
- no: 不自动装配，需要使用 `<ref />`节点或参数
- byName: 根据名称进行装配
- byType: 根据类型进行装配
- constructor: 根据构造函数进行装配


## Spring Boot、Spring Mvc 和 Spring 有什么区别?

- spring是一个IOC容器，用来管理Bean，使用依赖注入实现控制反转，可以很方便的整合各种框架，提供AOP机制弥补OOP的代码重复问题、更方便将不同类不同方法中的共同处理抽取成切面、自动注入给方法执行，比如日志、异常等


- springmvc是spring对web框架的一个解决方案，提供了一个总的前端控制器Servlet，用来接收请求，然后定义了套路由策略(url到handle的映射)及适配执行handle，将handle结果使用视图解析技术生成视图展现给前端

- springboot是spring提供的一个快速开发工具包，让程序员能更方便、更快速的开发spring+springmvc应用，简化了配置(约定了默认配置)，整合了一系列的解决方案(starter机制)、redis、mongodb、es，可以开箱即用


## SpringMVC工作流程


![[Pasted image 20240427193048.png]]

![[Pasted image 20240427193205.png]]



## SpringMVC核心组件

![[Pasted image 20240427200716.png]]


## Springboot自动装配

![[Pasted image 20240427201644.png]]

如图所示:
![[Pasted image 20240427201830.png]]


![[Pasted image 20240427201703.png]]


## 如何理解 Spring Boot 中的 starter
假如使用spring+springmvc，需要引入mybatis等框架，则要到xml中定义mybatis需要的bean-starter就是定义一个starter的jar包.

写一个@Configuration配置类、将这些bean定义在里面，然后在starter包的META-INF/spring.factories中写入该配置类.

springboot会按照约定来加载该配置类开发人员只需要将相应的starter包依赖进应用，进行相应的属性配置(使用默认配置时，不需要配置)，就可以直接进行代码开发，使用对应的功能了，比如mybatis-spring-boot--starter，spring-boot-starter-redis





