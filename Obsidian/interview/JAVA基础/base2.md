## 反射

```java
//获取反射的三种方式  
Class<?> Clazz1 = Class.forName("ling.Student"); 

Class<Student> Clazz2 = Student.class;  

Class<? extends Student> Clazz3 = new Student().getClass();
```

`java.lang.reflect.Modifier` 类中定义的修饰符常量及其值：

- public:  1
- private: 2
- protected: 4
- static: 8
- final:  16
- synchronized:  32
- volatile:  64
- transient:  128
- native:  256
- interface:  512
- abstract: 1024
- strictfp: 2048

#### Method

```java
Method method = Clazz3.getMethod("run", String.class);  
Student s = new Student();  
method.invoke(s,"400米长跑");
```

其中,invoke方法中的参数包括以下几个方面:
1. s : 方法调用者,一般为对象
2. 方法所需要的参数,一般为可变参数


## 集合


### collection
![[Pasted image 20240501214422.png]]


### map
![[Pasted image 20240501214451.png]]



