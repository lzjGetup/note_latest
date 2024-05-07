## 监控与日志

#### 容器日志驱动
在启动容器时,可以通过`--log-driver`选项配置日志驱动,常用的日志驱动如下:

![[Pasted image 20240422192540.png]]




#### 查看容器中运行的进程的信息
可以使用 docker top 命令查看容器中正在运行的进程的信息，语法如下
```c
docker top 容器[ps 选项]
```

可以运行以下命令行脚本来查看所有正在运行的容器中的进程信息

```c
for i in `docker ps |grep Up | awk '{print $1}'`;do echo \&&docker top $i; done
```


#### 查看容器的资源使用情况
可以使用 `docker stats` 命令实时查看容器的系统资源使用情况，语法如下:
`docker stats[选项][容器…]`

主要选项说明如下:
--al(-a):显示所有的容器，包括未运行的。默认仅显示正在运行的容器。
--fommat:根据指定格式显示内容。
--no-stream:仅显示第1条记录(只输出当前的状态)。
--no-trunc:不截断输出，显示完整的信息。



#### 使用cAdvisor监控容器

cAdvisor是一个开源的docker容器监控软件,用以下命令进行配置


```c
docker run --privileged \
--volume /:/rootfs:ro \
--volume /var/run:/var/run:rw \
--volume /sys:/sys:ro \
--volume /var/lib/docker/:/var/lib/docker:ro \
--publish 8080:8080 \
--detach \
--name cadvisor \
google/cadvisor:latest

```


其中 4个-volume 选项所定义的绑定挂载都不能缺少，否则会无法连接到Docker守护进程，--publish 8080:8080 选项表示对外暴露端口 8080 以提供服务;--detach 选项表示容器创建以后以分离方式在后台运行，让其自动完成监视功能。

部分docker参数 : 
![[Pasted image 20240422202619.png]]


这些参数描述了 Docker 容器运行时的一些配置和环境信息，下面是对这些参数的解释：

1. **Storage Driver**：指定了 Docker 使用的存储驱动程序。在这里，`overlay2` 是一种常用的存储驱动，它提供了高性能的联合文件系统支持，适用于大多数生产环境。
    
2. **Backing Filesystem**：指定了容器所在的文件系统类型。在这里，`xfs` 是 Linux 上一种常用的高性能文件系统。
    
3. **Supports d_type**：表示文件系统是否支持 `d_type` 特性，这对于某些容器操作是必要的。在这里，`true` 表示文件系统支持 `d_type` 特性。
    
4. **Using metacopy**：表示是否使用了元数据拷贝功能。在某些文件系统中，元数据拷贝可以提高文件拷贝的性能。在这里，`false` 表示未使用元数据拷贝。
    
5. **Native Overlay Diff**：表示是否启用了原生的 Overlay Diff。Overlay Diff 是 overlay2 存储驱动的一种优化技术，用于在容器之间共享文件系统层，提高了容器的启动速度和存储效率。在这里，`true` 表示已启用。
    
6. **userxattr**：表示文件系统是否支持用户扩展属性。在这里，`false` 表示不支持。


![[Pasted image 20240422203549.png]]


#### logs

`docker logs` 命令用于查看容器的日志输出。以下是 `docker logs` 命令的常用选项及其释义：

1. **-f, --follow**：实时跟踪容器的日志输出，类似于 `tail -f` 命令，可用于持续监视容器的输出。
    
2. **--since**：仅显示指定时间后的日志。可以接受绝对时间（如"2022-01-01T00:00:00"）或相对时间（如"10m" 表示过去10分钟）。
    
3. **--tail**：仅显示指定行数的日志，默认为所有日志。例如，`--tail 100` 将仅显示最后100行日志。
    
4. **--timestamps**：在日志中显示时间戳。
    
5. **--details**：显示更多的容器日志详情，包括标准输出和标准错误。
    
6. **--since-id**：仅显示指定 ID 后的日志，可以指定容器的短 ID 或完整 ID。
    

这些选项可以单独使用，也可以组合使用，以满足特定的日志查看需求。例如，`docker logs -f --tail 100 container_name` 将实时跟踪容器名为 `container_name` 的日志，并仅显示最后100行。


#### 日志驱动

可以在`/etc/docker/daemon.json`文件中配置docker的日志驱动, 默认的日志驱动为json-file. 另外在启动容器时,可以通过--log-driver 选项将其配置成与docker守护进程不同的日志驱动.

#### 日志清理
##### 清理脚本
容器的日志文件会占据大量的磁盘空间。在 Linux 中，容器日志一般存放在/var/ib/docker/containers/container_id 目录下以json.log 结尾的文件中。如果容器正在运行,那么使用 Linux 系统的rm -rf命令删除日志后，通过 df-h命令检查会发现磁盘空间并没有释放，除非重启 Docker。这是因为日志文件是被打开的(有进程正在使用)，进程将仍然可以读取该文件，磁盘空间也一直被占用。正确的日志清理方法是将日志文件清空，这里提供一个shel 脚本清理正在运行的容器的日志。



```bash
#!/bin/sh
logs=$(find /var/lib/docker/containers/ -name *-json.log)
for log in $logs
	do
		echo "clean logs :$log"
		cat /dev/null>$log
	done
```


##### 清理配置
要从根本上解决日志占用空间问题，就需要限制容器的日志大小上限。
在 daemon.json 配置文件为 Docker 守护进程设置日志驱动时，可以通过log-opts 选项来限制日志大小的上限。
例如:
```json
"log-driver":"json-fle",
"log-opts": {"max-size":"500m", "max-file":"2"}
```
上述设置表明默认的容器日志大小上限是 500MB，一个容器最多有2个日志文件

#### 容器日志记录到journald

`journald` 是 systemd 中的一个日志记录服务，用于管理系统日志。它是 systemd 的一部分，负责收集、存储和管理系统日志。

选择journald作为日志驱动可将日志定向输出到systemd系统日志
```c
docker run -d --name test --log-driver journald redis
```
