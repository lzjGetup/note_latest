## 初始

>![[Pasted image 20240125210009.png]]


>![[Pasted image 20240125210452.png]]

>![[Pasted image 20240125211938.png]]

>![[Pasted image 20240125212213.png]]

##### 安装见md文档

## 简单命令

>![[Pasted image 20240126110325.png]]

>![[Pasted image 20240126112706.png]]

>![[Pasted image 20240126113436.png]]

## 进入容器

>![[Pasted image 20240126114724.png]]

## 数据卷

>![[Pasted image 20240126122406.png]]

## 目录挂载

  
Docker中有两种常见的目录挂载方式：宿主机挂载和Docker自动创建模式。

1. 宿主机挂载： 在宿主机挂载中，你可以将宿主机上的一个目录挂载到Docker容器中。这样做可以让容器中的数据持久化保存在宿主机上，即使容器被删除，数据仍然存在于宿主机上。你可以使用-v参数来实现宿主机挂载，例如：

```c
docker run -v /host/directory:/container/directory image_name
```

2. Docker自动创建模式： 在Docker自动创建模式中，Docker会自动在宿主机上创建一个目录，并将容器中的数据保存在这个目录中。这种方式适合于一些临时性的数据存储需求，因为当容器被删除时，这个目录也会被自动清理掉。

## 自定义镜像

>![[Pasted image 20240127192545.png]]

###### DockerFile

>![[Pasted image 20240127192918.png]]



>![[Pasted image 20240127193750.png]]

##### DockerCompose

>![[Pasted image 20240127194317.png]]

##### Maven配置打包名称

finalName最终名称

>![[Pasted image 20240127195630.png]]

### 搭建私有仓库
见MD文档

更改tag;拉取,推送镜像

>![[Pasted image 20240127200918.png]]











