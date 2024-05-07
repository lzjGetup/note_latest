## Docker配置

#### 启用实时恢复功能
有两种方式可以启用实时恢复功能，使容器在守护进程不可用时保持活动状态。
一种方式是在Docker 守护进程配置文件(在 Linux 系统上默认是/etc/docker/daemon.json)中进行设置，加入以下选项。
```c
{
	"live-restore": true
}
```

重启 Docker 守护进程。
在 Linux 主机上可以通过重新加载 Docker 守护进程来避免重启 Docker(同时避免容器停止 )。如果使用 systemd，则使用 ==systemctl reload docker== 命令即可。否则，向 dockerd 进程发送 SIGHUP信号，具体方法是执行以下命令。
`kill -SIGHUP dockerd`
另一种启用实时恢复的方式是在手动启动 dockerd 进程时指定
`--live-restore` 选项。这里不建议使用此方法，因为它不会在启动 Docker 进程时设置 systemd 或其他进程管理器所使用的环境，这可能会导致意外行为的发生。



#### 容器健康检查

##### (1)在 Dockerfle 中使用 HEALTHCHECK指令
可以在 Dockerfle 文件中使用 HEALTHCHECK 指令声明健康检测配置，用于判断容器主进程的服务状态是否正常，反映容器的实际健康状态。

基于这样的 Dockerfile 构建镜像，再基于该镜像启动容这样的容器就具备健康状态检查能力，能够自动进行健康检查。
HEALTHCHECK 指令包括以下两种格式。
```c
HEALTHCHECK[选项]CMD<命令>
HEALTHCHECK NONE
```

第1种格式表示设置检查容器健康状况的命令;
第2种格式表示禁止从基础镜像继承HEALTHCHECK指令设置。


这里重点介绍第1种，其中可用的选项如下
- --interval:设置容器运行之后开始健康检查的时间间隔，默认为 30s。
- --timeout:设置允许健康检查命令运行的最长时间，默认为 30s。如果超时，本次健康检查就被视为失败。
- --start-period:设置需要启动的容器的初始化时间，在启动过程中的健康检查失败不会被计入默认为 0s。
- --retries:设置允许连续重试的次数，默认为3次。当健康检查连续失败指定的次数后，则将容器状态视为不健康状态。

下面的示例表示每 5min 执行一次健康检查，通过访问 Web 服务器主页进行检查，每次检查执行时间限制在 3s 以内。
```c
HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1
```


##### (2)启动容器时通过相应选项实现健康检查

可以在执行 `docker run` 命令时启动容器,或者执行`docker create` 命令创建容器时通过相应选项指定容器的健康检查策略，其中--health-cmd 选项用于指定健康检查命令，对应于Dockerfile 中HEALTHCHECK 指令的命令参数;
--health-interval、--health-retries、--health-timeout 和--health-start-period 分别对应于 Dockerfle 中 HEALTHCHECK 指令的--interval、--retries.--timeout和--start-period 选项。
--no-healthcheck 选项用于禁用容器的任何HEALTHCHECK指令


#### 容器重启策略

容器默认是不支持自动重启的。要为容器配置重启策略，可以在执行 docker  run 或 docker create命令启动或创建容器时使用--restart 选项。该选项的可用值如下表所示。

>![[Pasted image 20240422161759.png]]

对于已经创建或者运行的容器,可以通过docker update命令来更改其重启策略,例如:
```c
docker update --restart=on-failure:3 35vdfdf24v
```


#### 容器内存限制

1.  -m(--memory): 设置容器可用最大内存
2.  --memory-swap: 允许容器置入磁盘交换空间中的内存大小
通常情况下,默认交换空间为内存的两倍
![[Pasted image 20240422165648.png]]


```c
1. 300M 的内存
docker run -m 300M --memory-swap -1 centos
2. 400M 的交换空间//2*400-400=400m
docker run -m 400M centos
3. 300M 的内存 400M 的交换空间
docker run -m 300M --memory-swap 700M centos
```

#### 内存预留

内存预留是一种软限制, 内存预留值应当始终低于硬限制，否则硬限制会优先触发。将内存预留值设置为0表示不作限制。
默认情况下没有设置内存预留。

作为一个软限制功能，内存预留并不能保证不会超过限制。它主要的目的是确保当内存争用严重时，内存就按预留设置进行分配。
以下示例限制内存为 500MB，内存预留值(软限制)为200MB。
```c
docker run -m 500M--memory-reservation 200M ubuntu
```
按照此配置，当容器消耗内存大于 200MB、小于 500MB 时，下一次系统内存回收将尝试将容器内存缩减到 200MB 以下。


#### CPU 限制

##### CPU份额限制
默认情况下，所有的容器都得到相同比例的 CPU 周期。可以更改这个比例，设置一个容器相对于所有其他正在运行的容器的 CPU 份额权重。
使用`-c(--cpu-shares)`选项将 CPU 份额权重设置为指定的值。默认值为 1024,如果设置为 0系统将忽略该值并使用默认值 1024。


##### CPU 周期限制
使用`--cpu-period `选项(以μs 为单位)设置 CPU 周期以限制容器 CPU 资源的使用。默认的CFS(完全公平调度器)周期为100ms。
通常将--cpu-period与--cpu-quota 这两个选项配合使用。这里给出一个示例。
```c
docker run --cpu-perod=50000 --cpu-quota=25000 ubuntu
```

此例表明，如果只有1个CPU，则容器可以每50ms(50000us)获得50%(25000/50000)的 CPU 运行时间。

还可以使用`--cpus`选项,达到同样目的, 其值为一个浮点数, 默认值为0.000, 表示不作限制
```c
docker run --cpus 0.5 ubuntu
```


##### CPU 放置限制
可以通过`--cpuset-cpus` 选项限制容器进程在指定的 CPU上执行。下面的示例表示容器中的选可以在 cpu 1 和 cpu 3上执行。
```c
docker run --cpuset-cpus="1,3" ubuntu:14.04
```
再来看一个示例，容器中的进程可以在cpu0、cpu1和 cpu2 上执行。
```c
docker run --cpuset-cpus="0-2" ubuntu:14.04
```