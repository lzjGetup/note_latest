## Method

#### 固定参数
```java
@Query("select u from User u where u.userName='zhangsan'")  
List<User> findAllByUserName();
```

#### 占位传参

```java
@Query("update User set userName=?2 where id=?1")  
@Modifying  
@Transactional  
Integer updateUserNameById(Integer id,String username);
```

#### 集合遍历
```java
@Query(value = "select * from user where id in :ids", nativeQuery = true)  
List<User> getUserByIdIs(@Param("ids") List<Integer> ids);
```