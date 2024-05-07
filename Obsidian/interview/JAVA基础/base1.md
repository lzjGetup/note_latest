## Static

![[Pasted image 20240501155151.png]]



### 注意事项

- **静态**方法只能访问静态变量和静态方法
- **非静态**方法可以访问静态变量或者静态方法，也可以访问非静态的成员变量和非静态的成员方法
- 静态方法中是没有**this**关键字

## 权限修饰符的分类

![[Pasted image 20240501155656.png]]


## 代码块

### 局部代码块
```java
public static void main(String[] args) {  
    {  
        int a = 10;  
    }  
    System.out.println(a);  
}
```

此处的a变量将无法访问,在局部代码块结束以后,a变量将被内存回收.


### 构造代码块
对于构造方法中相同的部分,可以提取出来,在构造代码块中进行描述. 其中的内容会在所有的构造方法前执行

```java
public class Student {  
    private String name;  
    {  
        System.out.println("开始构造对象了");  
    }  
    public Student() {  
    }  
    public Student(String name) {  
        this.name = name;  
    }
}
```


### 静态代码块

特点: 需要通过static关键字修饰，随着类的加载而加载，并且自动触发、只执行一次
使用场景: 在类加载的时候，做一些数据初始化的时候使用

```java
static {}
```


## 内部类

### 成员内部类

![[Pasted image 20240501163344.png]]

构造与创建

```java
public class Car {  
    class Engine {  
    }  
}

```

获取成员心部类对象的两种方式:
方式一:外部类编写方法，对外提供内部类对象(private修饰下)
方式二:直接创建
```java
//注意: 需要在同一个包下才可行
Car.Engine engine = new Car().new Engine();
```

### 静态内部类

构造
```java
public class Car {  
    private String name;  
    static class Engine {  
        private String power;  
        public static void show(){}  
        public void run(){}  
    }  
}
```

使用
```java
public static void main(String[] args) {  
    Car.Engine engine = new Car.Engine();  
    Car.Engine.show();  
    engine.run();  
}
```

其中可以看出,静态内部类的创建是由`new Outer.inner`实现的;
静态方法直接点出
普通成员方法,用对象调用


### 匿名内部类
```java
new 类名或者接口名(){
	//重写方法;
};
```

其中:
1. `{}`之间为内部类,如果是抽象类或者接口应该重写方法
2. `new XXX();`为创建对象的形式,表明创建匿名内部类; 所以,以上代码具体来说,是创建了匿名内部类的对象

