## 反编译
在IDEA类文件中,右键打开于explorer中,找到项目根目录下的out文件夹,找到需要反编译的字节码文件;随后在cmd中,用`javap + 文件名`进行反编译即可


## 内存分析

![[Pasted image 20240501181253.png]]


`jps` 和 `jhsdb hsdb` 是与 Java 相关的两个命令行工具，主要用于诊断和分析 Java 应用程序的运行状态。下面我将分别介绍这两个工具。

#### 1. jps (Java Virtual Machine Process Status Tool)

`jps` 是 Java 虚拟机进程状态工具，用于列出当前正在运行的 Java 虚拟机的进程和它们的主要类（或者是 JAR 归档）名以及这些进程的 JVM 参数。这个工具对于确定系统上运行的 Java 进程非常有用。

**基本用法**：

```bash
jps
```

运行 `jps` 后，你将看到类似以下的输出：

```bash
23456 MyJavaApp  
23457 Jps
```

其中，数字是进程 ID，后面的字符串是 Java 应用程序的主类名或 JAR 文件名。

**高级用法**：

- 使用 `-l` 选项输出完整的包名和类名：
- 使用 `-m` 选项输出传递给主方法的参数：
- 使用 `-v` 选项输出传递给 JVM 的参数：


#### 2. jhsdb hsdb (Java HotSpot Serviceability Debugger with HotSpot Debugger Interface)

`jhsdb` 是 Java HotSpot 调试器，它提供了许多用于诊断和分析 HotSpot JVM 的功能。其中，`hsdb` 是 `jhsdb` 的一个图形界面工具，它允许你通过图形界面来查看和分析 JVM 的内部状态。

**基本用法**：

要启动 `hsdb` 并连接到正在运行的 JVM，你需要知道要连接的 JVM 的进程 ID。然后，你可以使用以下命令：

```bash
jhsdb hsdb --pid <process_id>
```

其中，`<process_id>` 是你想要连接的 JVM 的进程 ID。

**高级用法**：

- 你可以使用其他选项来连接到 JVM，例如通过核心转储文件或远程连接。
- 在 `hsdb` 的图形界面中，你可以查看各种有关 JVM 的信息，如线程堆栈、堆内存使用情况、类加载器层次结构等。
- 你还可以使用 `hsdb` 来执行各种诊断命令，如打印线程堆栈、触发垃圾收集等。
