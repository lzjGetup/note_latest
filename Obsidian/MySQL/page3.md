# SQL优化
### insert优化

1. 批量插入
2. 手动事务
3. 主键顺序插入

**大批量插入数据**
可以采用加载本地文件的方式进行

>![[Pasted image 20240228140559.png]]


### 主键优化

>![[Pasted image 20240228142734.png]]

>![[Pasted image 20240228142313.png]]

`主键设计原则`
1. 满足业务需求的情况下，尽量降低主键的长度。
2. 插入数据时，尽量选择顺序插入，选择使用AUTOINCREMENT自增主键。
3. 尽量不要使用UUID做主键或者是其他自然主键，如身份证号。
4. 业务操作时，避免对主键的修改。


### order by优化

1. Using filesort:通过表的索引或全表扫描，读取满足条件的数据行，然后在排序缓冲区sort buffer中完成排序操作，所有不是通过索引直接返回排序结果的排序都叫 FileSort 排序。
2. Using index:通过有序索引顺序扫描直接返回有序数据，这种情况即为using index，不需要额外排序，操作效率高。

- 对于联合索引,创建时可以指定每个字段索引分别按照升序或者降序排序.
- 倘若用orderby进行搜索时,`每个需要搜索的字段均为升序或者降序`,用explain进行分析DQL语句时,Extra内容栏显示Using index,否则为Using index和Using filesort.

如果不可避免的出现filesort，大数据量排序时，可以适当增大排序缓冲区大小 sort buffer size(默认256k)。


### group by优化
在分组操作时，可以通过索引来提高效率
分组操作时，索引的使用也是满足最左前缀法则的。

### limit优化

![[Pasted image 20240228151921.png]]

### count优化
![[Pasted image 20240228152142.png]]

![[Pasted image 20240228152801.png]]

### update优化

InnoDB的行锁是针对索引加的锁，不是针对记录加的锁,并且该索引不能失效，否则会从行锁升级为表锁










