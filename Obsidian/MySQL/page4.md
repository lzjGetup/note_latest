# 视图

- 视图(View)是一种虚拟存在的表。视图中的数据并不在数据库中实际存在，行和列数据来自定义视图的查询中使用的表，并且是在使用视图时动态生成的。

- 通俗的讲，视图只保存了查询的SOL逻辑，不保存查询结果。所以我们在创建视图的时候，主要的工作就落在创建这条SQL查询语句上

### 视图的检查选项

当使用WITH CHECK OPTION子句创建视图时，MySQL会通过视图检查正在更改的每个行，例如 插入，更新，删除，以使其符合视图的定义。
MySQL允许基于另一个视图创建视图，它还会检查依赖视图中的规则以保持一致性。为了确定检查的范围，mysql提供了两个选项:CASCADED 和 LOCAL，默认值为CASCADED。


- cascaded:  如果当前视图有检查选项，则插入数据要满足包括当前视图条件以及满足当前视图所依赖的视图的条件。
- 如果当前视图没有检查选项，则插入数据要满足当时视图所依赖视图有检查选项及其依赖的视图的条件。

- local检查选项是递归的查找当前视图所依赖的视图是否有检查选项，如果有，则检查；如果没有，就不做检查。


### 视图更新

![[Pasted image 20240229111444.png]]
## 作用

1. 简单
视图不仅可以简化用户对数据的理解，也可以简化他们的操作。那些被经常使用的查询可以被定义为视图，从而使得用户不必为以后的操作每次指定全部的条件。
2. 安全
数据库可以授权，但不能授权到数据库特定行和特定的列上。通过视图用户只能查询和修改他们所能见到的数据;
3. 数据独立
视图可帮助用户屏蔽真实表结构变化带来的影响

# 变量
用户定义变量 是用户根据需要自己定义的变量，用户变量不用提前声明，在用的时候直接用“@变量名”使用就可以。其作用域为当前连接。

### 局部变量

![[Pasted image 20240229133657.png]]

# 存储过程

- 存储过程是事先经过编译并存储在数据库中的一段SQL语句的集合，调用存储过程可以简化应用开发人员的很多工作，减少数据在数据库和应用服务器之间的传输，对于提高数据处理的效率是有好处的。
- 存储过程思想上很简单，就是数据库 SQL语言层面的代码封装与重用。 


## 参数
![[Pasted image 20240229142622.png]]
`in为默认参数`

## If,Case,While,Repeat,Loop

```sql
CREATE PROCEDURE p(in score int, out result varchar(10))
BEGIN 
	if score >= 80 then
		set result = "优秀";
	elseif score >=60 then
		set result = "良好";
	else 
		set result = "不及格";
	end if;
END;

CALL p(59,@result);
select @result;
--不及格
```

```sql
CREATE PROCEDURE p
BEGIN
	case
		when month >= 1 and month <= 3 then 
		set result = "第一季度";
END;
```

```sql
CREATE PROCEDURE p(in n int)
BEGIN
	declare total int default 0;
	while n > 0 do
		set total = total + n;
		set n = n - 1;
	end while;
	select total;
END;
```

```sql
CREATE PROCEDURE p(in n int)
BEGIN
	declare total int default 0;
	repeat
		set total = total + n;
		set n = n - 1;
	until n<=0
	end repeat;
	select total;
END;
```

##### loop
![[Pasted image 20240229144245.png]]

## 游标

将tb_user的记录筛选后写入tb_user_pro;
**图片有误:此处变量的声明应该在游标的声明之前,且无条件处理,游标读取最后一条数据后会报错**


![[Pasted image 20240229151944.png]]


![[Pasted image 20240229152013.png]]

**退出条件处理**
`declare exit handler for SQLSTATE'02000'close u_cursor;`

>![[Pasted image 20240229152602.png]]


