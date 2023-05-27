# Mysql家里学补充

## 13.分组数据

主要是GROUP BY 和HAVING子句

分组语句的使用：

```sql
SELECT vend_id,COUNT(*) AS num_prods
FROM products
GROUP BY vend_id;
```

GROUP BY必须在WHERE之后，ORDER BY之前。

where只能过滤指定，不能过滤分组。以此推出了HAVING。

**HAVING和WHERE的区别在于，where过滤行，而having过滤分组。**

如何过滤分组：

```sql
SELECT cust_id,COUNT(*) AS orders
FROM orders
GROUP BY cust_id
HAVING COUNT(*) >= 2;
```



ORDER BY和HAVING配合使用

```sql
SELECT order_num,SUM(quantity*item_price) AS ordertotal
FROM orderitems
GROUP BY order_num
HAVING SUM(quantity*item_price) >= 50
ORDER BY ordertotal;
```

以order_num分组，以ordertotal排序。对于分组中的筛选要用HAVING。



目前来看SELECT子句的顺寻：

1. SELECT
2. FROM
3. WHERE
4. GROUP BY
5. HAVING
6. ORDER BY
7. LIMIT

## 18.全文本搜索

数据库最常用的两个引擎：**MyISAM，和InnoDB**。**myisam支持全文本搜索，innodb不支持。**

全文本搜索用来解决like通配操作符和正则表达式匹配带来的性能开销大，明确控制不明等问题。

fulltext字句：

![2023-04-20 14:06:06.158000](file:///C:/Users/gaohan/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

在索引之后，使用Match（）和Against（）函数执行全文本搜索。Match指定被搜索到列，against指定要使用的搜索表达式。

```sql
select note_text

From productnotes

Where match(note_text) against(“rabbit”);
```



 

找到这行中有rabbit的，不区分大小写

全文本搜索的一个重要原因就是对结果排序，高优先级的先返回。文本词靠前的行的等级值比词靠后的行的等级高。

扩展搜索，找到一些有用的：

```sql
select note_text

From productnotes

Where match(note_text) against(“anvils” with query expansion);
```

也就是使用with query expansion。

 

 

方法3:布尔文本搜索

可以匹配词，排斥词，排列提示等。不需要fulltext索引也可以使用。

使用关键字： **IN BOOLEAN MODE**

![2023-04-20 14:50:40.257000](file:///C:/Users/gaohan/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)