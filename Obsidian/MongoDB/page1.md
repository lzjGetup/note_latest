# 简介

- MongoDB是一个介于关系数据库和非关系数据库之间的产品，是非关系数据库当中功能最丰富，最像关系数据库的。
- 它支持的数据结构非常松散，数据格式是BSON，一种类似ISON的二进制形式的存储格式，简称BinaryJSON，和ISON一样支持内嵌的文档对象和数组对象，因此可以存储比较复杂的数据类型。
- MongoDB最大的特点是它支持的查询语言非常强大，其语法有点类似于面向对象的查询语言几乎可以实现类似关系数据库单表查询的绝大部分功能，而且还支持对数据建立索引。**原则上 Oracle 和 MySQL 能做的事情,MongoDB 都能做(包括 ACID 事务)。**


|     $SQL概念$      |  $MongoDB概念$   |
| :--------------: | :------------: |
|  数据库(database)   | 数据库(database)  |
|     表(table)     | 集合(collection) |
|      行(row)      |  文档(document)  |
|    列(column)     |   字段(field)    |
|    索引(index)     |   索引(index)    |
| 主键(primary key)  |    _ id(字段)    |
|     视图(view)     |    视图(view)    |
| 表连接(table joins) | 聚合操作($lookup)  |
