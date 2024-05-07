## 命令

1. 列出可用版本
`yum list docker-ce --showduplicates | sort -r`

2. 安装特定版本
`yum install docker-ce<版本字符串>docker-ce-cli-<版本字符串>containerd.io`
中间一列,冒号后面截止到横杠前的.为版本字符串,eg 18.09.2

>![[Pasted image 20240413094124.png]]


3. 镜像 
`docker images `
- 显示镜像,完整id
--no-trunc
ID 采用UUID形式,唯一标识,64个16进制字符表示,sha256为哈希函数
过滤镜像
-f before/since = (镜像名,镜像id,镜像digest等)

4. Dockerfile构建
```c
FROM ubuntu:latest
COPY ./app /app
RUN apt-get -y update && apt-get install -y python
CMD python /app/app.py
```

该 Dockerfile 包括4个命令，每个命令创建一个层。
第 1  个命令表示从“ubuntu:16.04”镜像开始构建镜像。
第 2 个命令从 Docker 客户端的当前目录中添加一些文件。
第 3 个命令用于安装 Python。
最后一个命令指定要在容器中执行的具体命令。


5. 重命名容器
`docker rename <容器id> <新名字>`

6. 查看容器大小
`docker ps -s`

>![[Pasted image 20240413110649.png]]


SIZE 列第 1个值表示每个容器的可写层当前所用的数据大小。
第 2 个值是虚拟大小,位于括号中并标注 vrual，表示该容器所用只读镜像的数据量加上容器可写层大小的和。
多个容器可以共享一部分或所有的只读镜像数据，从同一镜像启动的两个容器共享100%的只读数据，而使用拥有公共镜像层的不同镜像的两个容器会共享那些公共的镜像层。
因此，不能只是汇总虚拟大小，这会导致潜在数据量的使用进而出现过高估计磁盘用量的问题。


7. 容器命令

>![[Pasted image 20240413111903.png]]

>![[Pasted image 20240413111941.png]]

8. 运行容器
`docker run`
-i(--interactive) : 让容器的标准输入打开,通常与-t 一同使用

-t(--tty) : 为容器分配一个伪输入终端(Pseudo TTY)

--dns : 指定容器使用的dns服务器,默认和主机上的dns保持一致.

9. Docker 后台运行的操作步骤:

- 检查本地是否存在指定的镜像，如果没有就从镜像仓库自动下载这个镜像
- 基于镜像创建一个容器并启动它。
- 为容器分配一个文件系统，并在镜像层顶部增加一个可读写的容器层。
- 从主机配置的网桥接口中将一个虚拟接口桥接到容器。
- 从网桥的地址池中给容器分配一个IP 地址。
-  运行用户指定的应用程序。
- 根据设置决定是否终止容器运行。

这种在后台运行容器的方式又称分离(Detached)模式，与之相对的是前台(Foreground)模式


10. 基于容器创建镜像
原理: 基于可写层的修改生成新的镜像,但是这种方式会使得镜像层数越来越多,由于联合文件系统允许的层数是有限的,所以不建议使用这种方式.

`docker commit [选项]容器 [仓库[:标签]]`
-a 指定提交的镜像作者
-c 使用dockerfile指令用于创建镜像
-p 执行提交命令commit时暂停容器

11. RUN,CMD,ENTRYPOINT
==RUN==
RUN 指令执行命令并创建新的镜像层，经常用于安装应用程序和软件包。
RUN 先于CMD 或ENTRYPOINT指令在构建镜像时执行，并被固化在所生成的镜像中。


CMD 和 ENTRYPOINT 指令在每次启动容器时才执行，两者的区别在于 CMD 指令会被 `docker run`命令所覆盖。
两个指令一起使用时，ENTRYPOINT 指令作为可执行文件，而 CMD 指令则为ENTRYPOINT 指令提供默认参数。

CMD 指令的主要作用是为运行容器提供默认值，即默认执行的命令及其参数，但当运行带有替代参数的容器时，CMD.指令将被覆盖。

如果CMD 指令省略可执行文件，则还必须指定ENTRYPOINT 指令。CMD 可以为ENTRYPOINT提供额外的默认参数，同时可利用docker run 命令替换默认参数。

当容器作为可执行文件时，应该定义 ENTRYPOINT 指令。ENTRYPOINT 指令配置容器启动时运行的命令，可让容器以应用程序或者服务的形式运行。

与CMD指令不同，ENTRYPOINT指令不会被忽略，一定会被执行，即使执行 docker nun 命令时指定了其他命令参数也是如此。如果 Docker 镜像的用途是运行应用程序或服务，如运行一个 MSQL 服务器，则应该优先使用 exec 格式的ENTRYPOINT指令。


