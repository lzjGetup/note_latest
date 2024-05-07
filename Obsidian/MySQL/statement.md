
- 查看建表语句: show create table 表名;
- 查看支持引擎: show engines;
- 查看变量: show variables like '变量名';
- 简单查看ibd文件: ibd2sdi 文件名
- 查看是否支持profile: select @@have_profiling;
- 设置profile: set (global/session) profiling = 1;
- 修改语句结束符 DELIMITER 符号


## 索引

- 创建索引
`CREATE [UNIQUE][FULLTEXT] INDEX index_name ON table_name (index_col_name,...);`

- 查看索引
`SHOW INDEX FROM table_name;`

- 删除索引
`DROP INDEX index_name ON table_name;`


## 视图
- 创建视图
`CREATE [OR REPLACE] VIEW 视图名称[(列名表名)] AS SELECT语句`

- 查询创建视图的语句
`SHOW CREATE VIEW 视图名`

- 查看视图数据
`SELECT * FROM 视图名`

- 修改视图
1. `CREATE VIEW 视图名称 AS SELECT语句`
2. `ALTER VIEW 视图名称 AS SELECT语句`

- 删除视图
`DROP VIEW[IF EXISTS] 视图名称...`

## 存储过程

#### 创建及使用

```sql
DELIMITER //

CREATE PROCEDURE GetExpensiveDishes()
BEGIN
    SELECT id, name, price
    FROM dish
    WHERE price >= 50;
END //

DELIMITER ;
CALL GetExpensiveDishes();
```

#### 查看存储过程
- 查询指定数据库的存储过程及状态信息
`SELECT * FROM INFORMATION SCHEMA.ROUTINES WHERE ROUTINE SCHEMA='xx';`

- 查询某个存储过程的定义
`SHOW CREATE PROCEDURE 存储过程名称;`

#### 删除
`DROP PROCEDURE 「IF EXISTS]存储过程名称`

## 变量

#### 赋值
直接赋值
`SET @var name = expr`
从表中获取字段赋值
`SELECT 字段名 INTO @var name FROM 表名;`
#### 使用
`SELECT @var name;`