# Nacos

## 启动

下载安装包后进入bin目录,输入命令,单机启动

```c
startup.cmd -m standalone
```

集群启动

```c
startup.cmd
```

## 注册与发现

1. 引入nacos.discovery依赖
2. 配置nacos地址spring.cloud.nacos.server-addr

## 配置集群属性

>![[Pasted image 20240125132854.png]]


## 权重配置

nacos权重可在控制台配置,权重值在0-1之间,权重为0则无法被访问.

## 环境隔离

在控制台可以设置命名空间,然后在代码的配置文件中修改即可划分命名空间

>![[Pasted image 20240125135040.png]]

>![[Pasted image 20240125134900.png]]

## 临时实例

对于服务列表的非临时实例,nacos会主动询问其健康,健康则重新加入到服务列表

>![[Pasted image 20240125141024.png]]


## 统一配置管理

对于需要根据环境,需求等去修改的配置,我们通常采用nacos统一配置管理,

>![[Pasted image 20240125142855.png]]

>![[Pasted image 20240125143005.png]]

nacos会先去bootstrap.yml文件中寻找统一配置,随后再将统一配置和本地配置结合,再启动服务

>![[Pasted image 20240125143043.png]]


## 配置自动更新

==属性更新==

1. 在`@value`属性注入所在的类上加入`@RefreshScope`注解,用于实现属性自动更新.

2. 编写配置类,类的顶部用`@ConfigurationProperties`注入,使用时,用`@Autowired`注入配置类使用get方法即可


## 多服务共享配置

优先级:
服务名-profile.yaml `>` 服务名.yaml `>` 本地配置

# Nacos集群配置

1. 先去配置集群ip地址信息,cluster.conf文件中

>![[Pasted image 20240125151747.png]]

2. 再去application.properties 文件中进行修改nacoss数据库配置信息,去掉#号配置生效
![[Pasted image 20240125152133.png]]




