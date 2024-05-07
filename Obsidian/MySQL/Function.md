# DATE
在MySQL 8.0中，有一些与日期数据类型相关的函数，包括：

1. CURDATE() - 返回当前日期。
2. NOW() - 返回当前日期和时间。
3. DATE() - 提取日期或日期时间表达式的日期部分。
4. EXTRACT() - 从日期或日期时间表达式中提取指定的字段。
5. DATE_ADD() - 给定日期添加一个指定的时间间隔。
6. DATE_SUB() - 从给定日期减去一个指定的时间间隔。
7. DATEDIFF() - 返回两个日期之间的天数差。
8. DATE_FORMAT() - 格式化日期或日期时间值。

DATE_ADD() 函数用于向日期添加一个指定的时间间隔，并返回计算后的日期。
```sql
DATE_ADD(date, INTERVAL expr type)
```
其中，date 是要进行计算的日期，expr 是要添加的时间间隔，type 是时间间隔的类型，可以是 MICROSECOND, SECOND, MINUTE, HOUR, DAY, WEEK


例如，如果要将某个日期加上一个月，可以这样使用 DATE_ADD() 函数：

```sql
SELECT DATE_ADD('2023-01-15', INTERVAL 1 MONTH);
```


# CASE

在MySQL中，CASE 表达式是一种条件语句，类似于其他编程语言中的 switch 语句。

```sql
SELECT
    customer_name,
    CASE
        WHEN age < 18 THEN '未成年'
        WHEN age >= 18 AND age < 65 THEN '成年人'
        ELSE '退休人员'
    END AS age_group
FROM
    customers;
```

# IF

在MySQL中，IF 函数是一种条件函数，它类似于其他编程语言中的三元运算符。

```sql
SELECT
    product_name,
    unit_price,
    IF(unit_price > 100, 'Expensive', 'Affordable') AS price_category
FROM
    products;
```

# ROUND

MySQL的ROUND函数用于将一个数值四舍五入到指定的小数位数。

```sql
ROUND(number, decimals)
```

```sql
SELECT ROUND(3.14159, 2);
//答案为3.14
```


# CROSS JOIN
在MySQL中，CROSS JOIN 是一种用于从一个表中选择所有行，并将其与另一个表中的所有行组合的方法。它会返回两个表的笛卡尔积，也就是说，它会返回第一个表的每一行与第二个表的每一行的组合。如果第一个表有m行，第二个表有n行，那么CROSS JOIN 将返回m.n行。

# USING
使用 using(product_id) 的作用是告诉数据库系统，product_id 列是 Orders 表和 Products 表中共有的列，因此在进行连接时，可以直接使用这个列进行匹配，而不需要使用 ON 子句来指定连接条件。这样可以简化查询语句，使其更易读和更简洁。





