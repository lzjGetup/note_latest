### 面向对象

![[Pasted image 20240418170332.png]]
##### 多态
多态是面向对象编程中一种重要的特性，它允许我们使用父类类型的引用变量来引用子类的对象，并调用子类的方法，从而提高了代码的扩展性和复用性。

### 抽象类与接口

![[Pasted image 20240418164108.png]]


### 重载与重写

![[Pasted image 20240418164206.png]]


### List&Set

![[Pasted image 20240418165908.png]]


### ArrayList&LinkedList
![[Pasted image 20240418165827.png]]

### HsahMap&HashTable

![[Pasted image 20240418171514.png]]

### ConcurrentHashMap
###### jdk7
![[Pasted image 20240418172730.png]]


###### jdk8
![[Pasted image 20240418172749.png]]

CAS是compare and swap的缩写，即我们所说的比较交换。cas是一种基于锁的操作，而且是乐观锁。在java中锁分为乐观锁和悲观锁。悲观锁是将资源锁住，等一个之前获得锁的线程释放锁之后，下一个线程才可以访问。而乐观锁采取了一种宽泛的态度，通过某种方式不加锁来处理资源，比如通过给记录加version来获取数据，性能较悲观锁有很大的提高。

### 如何实现一个IOC容器

![[Pasted image 20240423195903.png]]

### 什么是字节码,采用字节码的好处?

![[Pasted image 20240423200352.png]]


###  JAVA类加载器

![[Pasted image 20240423200726.png]]

### 双亲委派

![[Pasted image 20240423201306.png]]

![[Pasted image 20240423201531.png]]


### JAVA异常体系
![[Pasted image 20240423201918.png]]



### GC如何判断对象是否可以回收

![[Pasted image 20240423202623.png]]


### 线程生命周期

![[Pasted image 20240423203235.png]]


### sleep()、wait()、join()、yield()的区别

1. 锁池
所有需要竞争同步锁的线程都会放在锁池当中，比如当前对象的锁已经被其中一个线程得到，则其他线程需要在这个锁池进行等待，当前面的线程释放同步锁后锁池中的线程去竞争同步锁，当某个线程得到后会进入就绪队列进行等待cpu资源分配。
2. 等待池
当我们调用wait()方法后，线程会放到等待池当中，等待池的线程是不会去竞争同步锁。只有调用了 notify() 或 notifyAIl() 后等待池的线程才会开始去竞争锁，notify()是随机从等待池选出一个线程放到锁池，而notifyAIl()是将等待池的所有线程放到锁池当中


![[Pasted image 20240423204933.png]]


yield ()执行后线程直接进入就绪状态，马上释放了cpu的执行权，但是依然保留了cpu的执行资格，所以有可能cpu下次进行线程调度还会让这个线程获取到执行权继续执行

join ()执行后线程进入阻塞状态，例如在线程B中调用线程A的join()，那线程B会进入到阻塞队列，直到线程A结束或中断线程










