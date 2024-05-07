## 一对多

```java
@Entity
public class Parent {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @OneToMany(mappedBy = "parent", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Child> children = new ArrayList<>();
    
    // Constructors, getters, and setters
}

@Entity
public class Child {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @ManyToOne
    @JoinColumn(name = "parent_id")
    private Parent parent;
    
    // Constructors, getters, and setters
}

```

在这个示例中：

- `Parent` 类拥有一个被 `@OneToMany` 注解标记的子对象列表 `children`。`mappedBy = "parent"` 表示这个关系由 `Child` 实体中的 `parent` 属性来维护。
- `Child` 类拥有一个被 `@ManyToOne` 注解标记的父对象引用 `parent`。`@JoinColumn(name = "parent_id")` 定义了外键列的名称，用于在数据库中保存父对象的引用。
- 使用 `cascade = CascadeType.ALL` 表示当父对象被删除时，其关联的子对象也会被删除。`orphanRemoval = true` 表示当子对象从父对象的集合中移除时，它会被删除。

```java
// 创建父对象及其子对象
Parent parent = new Parent();
Child child1 = new Child();
Child child2 = new Child();

// 建立父子关系
parent.getChildren().add(child1);
parent.getChildren().add(child2);
child1.setParent(parent);
child2.setParent(parent);

// 保存父对象，这将会同时保存子对象
parentRepository.save(parent);
```


