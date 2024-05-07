# 搭建

1. 引入依赖
>![[Pasted image 20240125163905.png]]

2. 新模块编写启动类
3. 配置文件中添加nacos地址以及网关路由
4. 可选配置网关过滤器以及断言


>![[Pasted image 20240125170050.png]]
>

默认过滤器(全局作用)

![[Pasted image 20240125170455.png]]


==全局过滤器(可实现业务逻辑)==

继承`GlobalFilter`接口,实现`filter`方法即可

过滤器大致逻辑,注意应该在顶部添加`@compoment`注解实现spring管理.

另外,`@Order()`括号加入参数int类型,即可设置过滤器顺序,也可以通过继承`Ordered`接口实现方法

>![[Pasted image 20240125171359.png]]

## 过滤器排序规则

>![[Pasted image 20240125172503.png]]

## 跨域问题处理

>![[Pasted image 20240125205001.png]]


