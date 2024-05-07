## 自建docker注册中心
1. 创建启动一个运行docker registry
```c
docker run -d -p 5000:5000 --restart=always --name myregistry -v /opt/data/registry:/var/lib/registry registry
```

2. 测试
```c
curl http://127.0.0.1:5000/v2/_catalog
```

出现一下,表明没问题
![[Pasted image 20240413143633.png]]


3. 对镜像打上标签
```c
docker tag hello-world:latest 127.0.0.1:5000/hello-world:v1
```

4. 推送/拉取 镜像
```c
docker push/pull 127.0.0.1:5000/hello-world:v1
```



结果:
![[Pasted image 20240413144110.png]]



5. 配置注册中心地址
默认情况下，注册中心地址使用localhost或 127.0.0.1是没有问题的。
如果要使用主机的域名或1P地址就会报出"http: server gave HTTP response to HTTPS client”这样的错误,这是因为 Docker自从 1.3.X版之后，访问 Docker 注册中心默认使用的是 HTTPS，但是搭建的私有注册中心默认使用的是 HTTP。

最简单的解决方案是修改 Docker 客户端的/etc/docker/daemon.json 文件，将要使用的注册中心域名或 IP 地址添加到 insecure-registies 列表中，以允许 Docker 客户端与该列表中的注册中心进行不安全的通信。
本示例中定义如下。

```c
"insecure-registries":["192.168.200.128:5000"]
```

注意: 没有其他配置项的话需要大括号



