# 行转列
题目:重新格式化表格，使得 **每个月** 都有一个部门 id 列和一个收入列。
[题目链接](https://leetcode.cn/problems/reformat-department-table/description/)

>![[Pasted image 20240109143047.png]]

答案:
![[Pasted image 20240109143408.png]]


**讲讲group by起的作用**
GROUP BY id 会使department表按照id分组，生成一张虚拟表（假想中的表）如下：
>![[Pasted image 20240109143830.png]]


在虚拟表中，所有id=1的revenue或者month数据都写在了同一个单元格中，如8000、7000、6000都是写在同一单元格内的。真正的表是不能这样写的，所以这种写法只存在于虚拟表中，帮助我们理解。

**讲讲case when的原理**
当一个单元格中有多个数据时，case when只会提取当中的第一个数据。

以CASE WHEN month='Feb' THEN revenue END 为例，当id=1时，它只会提取month对应单元格里的第一个数据，即Jan，它不等于Feb，所以找不到Feb对应的revenue，所以返回NULL。（可以试试把我上面答案里的sum()统统去掉，执行结果与预期不一样。错就错在当id=1时,Feb_Revenue和Mar_Revenue的值变成了NULL）

那该如何解决单元格内含多个数据的情况呢？答案就是使用聚合函数，聚合函数就用来输入多个数据，输出一个数据的。如SUM()或MAX()，而每个聚合函数的输入就是每一个多数据的单元格。

以SUM(CASE WHEN month='Feb' THEN revenue END) 为例，当id=1时，它提取的Jan、Feb、Mar，从中找到了符合条件的Feb，并最终返回对应的revenue的值，即7000。


