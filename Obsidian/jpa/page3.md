### 多对多

多对多关系表示两个实体之间存在相互关联，每个实体都可以与多个另一实体相关联。例如，在一个学生和课程的关系中，一个学生可以选修多门课程，而一门课程也可以被多个学生选修。

以下是一个简单的 Java 类示例来说明多对多关系：


```java
@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    
    @ManyToMany(cascade = { CascadeType.PERSIST, CascadeType.MERGE })
    @JoinTable(name = "student_course",
               joinColumns = @JoinColumn(name = "student_id"),
               inverseJoinColumns = @JoinColumn(name = "course_id"))
    private Set<Course> courses = new HashSet<>();
    
    // Constructors, getters, and setters
}

@Entity
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();
    
    // Constructors, getters, and setters
}

```


在这个示例中：

- `Student` 类有一个 `Set<Course>` 类型的属性 `courses`，它使用 `@ManyToMany` 注解来标记与课程的关系。`@JoinTable` 注解用于定义关联表的名称以及两个实体之间的外键列。`joinColumns` 定义了本实体在关联表中的外键列，`inverseJoinColumns` 定义了关联实体（课程）在关联表中的外键列。
- `Course` 类有一个 `Set<Student>` 类型的属性 `students`，它使用 `@ManyToMany(mappedBy = "courses")` 注解来指定关联关系由 `Student` 类中的 `courses` 属性来维护。