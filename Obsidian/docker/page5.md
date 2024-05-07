## Docker对象

1. join
使用 join 函数将一组字符串进行连接以创建单个字符串，它在列表中的每个字符串元素之间放置一个分隔符，如下以inspect命令为例:

其中re为容器名,`--format`固定搭配,==", "==为分隔符号, `--format '{{join .Args ","}}'`整体为模板
```c
 docker inspect --format '{{join .Args ","}}' re
```

2. json
使用 json 函数将元素编码为 JSON 字符串，修改template即可
```c
--format '{{json [参数]}}'
```

3. lower/(upper)
使用 lower函数将字符串转换为小写，如下所示
```c
--format '{{lower .Name}}'
```

4. split
使用 split 函数将字符串切分为由分隔符分隔的字符串列表，如下所示。

```c
--format '{{split(json [参数] "/")"/"}}'
```

5. title
使用 title 函数将字符串的首字母转为大写，如下所示
```c
--format '{{title [参数]}}'
```


### 对象标记

支持标记的每种类型的 Docker 对象都具有添加、管理和使用标记的机制，这种机制与特定对象类型相关。
镜像、容器、本地守护进程、卷和网络上的标记在对象的生命周期内是静态的，必须要重新创建对象才能改变这些标记，
而 Swamm 集群节点和服务上的标记则可以动态更新。这里给出一个简单的示例。首先为容器加上标记:
1. 添加标记
```c
docker run -d --name re --label lab redis
```
2. 使用标记
```c
docker ps --filter label=lab
```

### 删除未使用的对象

Docker 采用保守的方法清理未使用的对象(如镜像、容器、卷和网络),这通常被称为“垃圾回收”这些对象实际上不会被删除，除非明确要求 Docker 这样做，这就可能导致 Docker 额外占用磁盘空间对于每种对象类型，Docker都提供了一条 prune 命令。另外，可以使用 `docker system prune` 命令次性清理多种类型的对象。

![[1713851588026.png]]

在 Docker 17.06.0 及之前的版本中,该命令默认还会删除不用的卷。在 Docker `17.06.1`及更高版本中，必须为 docker system prune 命令明确指定`--volumes` 选项才会删除卷

### 从 Docker 守护进程获取实时事件

可以使用 `docker events` 命令査看 Docker 服务器端的各种事件信息,包括容器、镜像、插件、卷网络，以及 Docker 守护进程事件。
不同的对象具有不同的事件，以方便调试使用。该命令的语法如下`docker events「选项]`
-f选项表示根据条件过滤事件;
--since 选项表示显示自某个时间戳开始的所有事件;
--untl 选项表示显示截至指定时间的所有事件。如果没有提供
--since 选项，则这个命令将只返回新的事件或实时事件。

