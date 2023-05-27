# 数据库（Mysql）

看笔记：[sql_node/MySQL学习笔记.md at master · baa-god/sql_node · GitHub](https://github.com/baa-god/sql_node/blob/master/mysql/MySQL学习笔记.md)

数据库：数据库是“按照数据结构来组织、存储和管理数据的仓库”。是一个长期存储在计算机内的、有组织的、可共享的、统一管理的大量数据的集合。

虽然关系型数据库有很多，但是大多数都遵循SQL（结构化查询语言，Structured Query Language）标准。 常见的操作有查询，新增，更新，删除，求和，排序等。

**关系型数据库**：关系型数据库，存储的格式可以直观地反映实体间的关系。关系型数据库和常见的表格比较相似，关系型数据库中表与表之间是有很多复杂的关联关系的。 常见的有Mysql，SqlServer等。

用的Sql语言,要重点学习

启动Mysql：

```c
mysql -uroot -p0309xnxn.
```

## 1.终端中操作数据库

- 如何查询数据库服务器中所有的数据库

要加分号

```cpp
mysql> show databases
    -> ;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.04 sec)
```

- 如何选择操作哪个数据库：

```c
 use sys
```

- 查询记录：

```cpp
select * from ***(名字)
select * from ***(名字) where ***=1；
```

- 创建数据库：

```cpp
create database 名字;
```

- 查看数据库里面内容

```c
show tables;
```

- 往数据库中创建数据表

![image-20230227153330610](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230227153330610.png)

pet：表名，name..：是所有项名字，后面的是数据类型

```cpp
mysql> CREATE TABLE pet(
    -> name VARCHAR(20),
    -> owner VARCHAR(20),
    -> species VARCHAR(20),
    -> sex CHAR(1),
    -> birth DATE,
    -> death DATE);
Query OK, 0 rows affected (0.06 sec)

mysql> show tables;
+-----------------+
| Tables_in_lbwnb |
+-----------------+
| pet             |
+-----------------+
1 row in set (0.01 sec)
```



- 查看数据表具体结构：

```c
mysql> describe pet;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.05 sec)
```



- 往表中添加数据记录

 ![image-20230227160620103](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230227160620103.png)

```
mysql> INSERT INTO pet
    -> VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL)
    -> ;
Query OK, 1 row affected (0.04 sec)
```

- 往表中删除数据

```cpp
delete from pet where name='Puffball';
```

- 修改数据

```cpp
 update pet set name='旺旺才' where owner='周星驰';
```

增：insert，删：delete，改：update *** set，查：select





- mysql常用数据类型大致可以分为三类：数值、日期/时间和字符串(字符)类型。

  - 数值：插入的值不能超过范围

  | 类型         | 大小                                     | 范围（有符号）                                               | 范围（无符号）                                               | 用途            |
  | :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
  | TINYINT      | 1 Bytes                                  | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
  | SMALLINT     | 2 Bytes                                  | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
  | MEDIUMINT    | 3 Bytes                                  | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
  | INT或INTEGER | 4 Bytes                                  | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
  | BIGINT       | 8 Bytes                                  | (-9,223,372,036,854,775,808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
  | FLOAT        | 4 Bytes                                  | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
  | DOUBLE       | 8 Bytes                                  | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
  | DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |

  - data：日期类型

  ![image-20230227161413258](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230227161413258.png)

  - 字符串：

  ![image-20230227161602008](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230227161602008.png)





mysql建表约束：

- 主键约束

  - 能唯一确定一张表的一条记录，通过对某个字段添加约束，可以使得字段不重复且不为空.

  比如这个就是设置id不能为空，也不能重复。

  ```cpp
   create table user(
   	id int primary key,
       name varchar(20)
   );
  ```

  ![image-20230227163045732](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230227163045732.png)

  要创建两个约束：

  ----是联合主键，两个不要都一样就可以。只有俩个一样才会报错。如果不写在后面，在屁股后面跟的话，每个都不能重复

  ```cpp
   create table user2(
   	id int,
      name varchar(20),
   	password varchar(20),
      primary key(id,name)
   );
  ```

  

- 自增约束：auto_increment;

```cpp
 create table user3(
 	id int primary key auto_increment,
     name varchar(20)
 );

插入的时候
insert into user3 (name) values('zhangsan');
//只插入一个属性，主键属性会自动帮我们自增补全，比如有1-2，再插入就是3
```

如果一开始创建的时候忘记加主键约束了，可以通过alter table方法添加，如下：同理 也可以删除

```cpp
alter table user3 add primary key(id);
alter table user3 drop primary key(id);
```

使用modify修改字段，添加约束

```cpp
alter table user3 modify id int primary key;
```



- 外键约束：

涉及到两个表，一个父表 一个子表

foreign key(class_id) references classes(id)

主表里面没有的，子表不能插入和使用的。

删除的时候，如果子表用了父表的键，父表这个值不能被删除

```c
create table classes(
	id int primary key,
    name varchar(20)
);

create table students(
	id int primary key,
    name varchar(20),
    class_id int,
    foreign key(class_id) references classes(id)
);
```





- 唯一约束：

约束该字段的值不可重复

```cpp
 create table user3(
 	id int primary key auto_increment,
     name varchar(20),
     unique(name)
 );

alter table user5 add unique(name);
```

解除唯一约束：

```cpp
alter table user7 drop index name;
```



- 非空约束

修饰的字段不能为空-not_null

- 默认约束

插入字段的时候没有传值，会使用默认值,比如default 10，表示默认10。

```cpp
 create table user3(
 	id int,
     name varchar(20),
	 age int default 10
 );
```



### 数据表设计

数据库的三大设计范式：

- 第一范式（1NF）：数据表中的所有字段都是不可分割的原子值，字段值哈可以继续拆分的就不满足第一范式。

比如：中国浙江省杭州市拱墅区石祥路60号。这种就是字段值可以拆分的。



假设下面这个是支持第一范式，范式设计的越详细，对某些实际操作可能更好，但不一定都是好处。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230301154026464.png" alt="image-20230301154026464" style="zoom:75%;" />

- 第二范式

必须满足第一范式的情况下，第二范式要求，除主键外的每一列都必须完全依赖主键。

如果出现不完全依赖，只可能发生在联合主键的情况下。 

![image-20230301154555143](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230301154555143.png)

分成三个表，每个除了主键外的每一列都依赖主键。



- 第三范式：

必须先满足第二范式，然后除了主列外的其他列之间不能有传递依赖关系。 

![image-20230301154917289](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230301154917289.png)

比如这的customer_phone就依赖了customer_id，然后customer_id又依赖于order_id所以产生了多个依赖关系。



### 查询练习（查询语句的编写）：

- 查询指定数据：

```cpp
select name,sex,class from student;
```

- 查询teacher表中不重复的department列：

==distinct==：表示去重

```cpp
SELECT DISTINCT department FROM teacher;
//表示对department列去重
```

- 按区间查询：where表示带条件，

```cpp
SELECT * FROM score WHERE degree BETWEEN 60 AND 80;
SELECT * FROM score WHERE degree > 60 AND degree < 80;
```

- 查询或条件:
  - 同一个字段

```cpp
-- 查询 score 表中成绩为 85, 86 或 88 的行
-- IN: 查询规定中的多个值
SELECT * FROM score WHERE degree IN (85, 86, 88);
```

​	不同字段：

```cpp
-- 查询 student 表中 '95031' 班或性别为 '女' 的所有行
-- or: 表示或者关系
SELECT * FROM student WHERE class = '95031' or sex = '女';
```



- 升序降序查找：

==order by ** desc/asc==

```cpp
-- 以 class 降序的方式查询 student 表的所有行
-- DESC: 降序，从高到低
-- ASC（默认）: 升序，从低到高
SELECT * FROM student ORDER BY class DESC;
SELECT * FROM student ORDER BY class ASC;


-- 以 c_no 升序、degree 降序查询 score 表的所有行
SELECT * FROM score ORDER BY c_no ASC, degree DESC;
```



- 统计人数：count

```cpp
select count(*) from student where class='95031';
```



- 查询最高分

 ```cpp
 -- 查询 score 表中的最高分的学生学号和课程编号（子查询或排序查询）。
 -- (SELECT MAX(degree) FROM score): 子查询，算出最高分
 SELECT s_no, c_no FROM score WHERE degree = (SELECT MAX(degree) FROM score);
 ```

正常步骤：

```cpp
selct max(degree) from score;
select sno,cno from score where degree=(select max(degree) from score);
```

排序查询法：

```cpp
-- LIMIT r, n: 表示从第r行开始，查询n条数据
SELECT s_no, c_no, degree FROM score ORDER BY degree DESC LIMIT 0, 1;
```



- 查询每门课的平均成绩：

先group by按照c_no分组。

 ```c
 select avg(degree) from score where c_no='3-105';
 
 select c_no,avg(degree) from score group by c_no;
 ```



- 分组条件与模糊查询

  group by之后的条件只能用having不能用where

```cpp
-- 首先把 c_no, AVG(degree) 通过分组查询出来
SELECT c_no, AVG(degree) FROM score GROUP BY c_no
+-------+-------------+
| c_no  | AVG(degree) |
+-------+-------------+
| 3-105 |     85.3333 |
| 3-245 |     76.3333 |
| 6-166 |     81.6667 |
+-------+-------------+

-- 再查询出至少有 2 名学生选修的课程
-- HAVING: 表示持有
HAVING COUNT(c_no) >= 2

-- 并且是以 3 开头的课程
-- LIKE 表示模糊查询，"%" 是一个通配符，匹配 "3" 后面的任意字符。
AND c_no LIKE '3%';

-- 把前面的SQL语句拼接起来，
-- 后面加上一个 COUNT(*)，表示将每个分组的个数也查询出来。
SELECT c_no, AVG(degree), COUNT(*) FROM score GROUP BY c_no
HAVING COUNT(c_no) >= 2 AND c_no LIKE '3%';
+-------+-------------+----------+
| c_no  | AVG(degree) | COUNT(*) |
+-------+-------------+----------+
| 3-105 |     85.3333 |        3 |
| 3-245 |     76.3333 |        3 |
+-------+-------------+----------+
```



- 多表查询：

```cpp
SELECT name, c_no, degree FROM student, score 
WHERE student.no = score.s_no;


SELECT s_no, name as c_name, degree FROM score, course
WHERE score.c_no = course.no;
```

- 三表联合查询

```cpp
SELECT student.name as s_name, course.name as c_name, degree 
FROM student, score, course
WHERE student.NO = score.s_no
AND score.c_no = course.no;
```

**查询 `95031` 班学生每门课程的平均成绩。**

```cpp
SELECT no FROM student WHERE class = '95031'//把这个当成条件放进去

SELECT c_no, AVG(degree) FROM score
WHERE s_no IN (SELECT no FROM student WHERE class = '95031')
GROUP BY c_no;
+-------+-------------+
| c_no  | AVG(degree) |
+-------+-------------+
| 3-105 |     82.0000 |
| 3-245 |     71.5000 |
| 6-166 |     80.0000 |
+-------+-------------+
```



- 子查询：

```
select degree from score where c_no='3-105' and s_no='109';
select * from score where degree >(select degree from score where c_no='3-105' and s_no='109');
```

**查询所有和 `101` 、`108` 号学生同年出生的 `no` 、`name` 、`birthday` 列。**

一般都无脑用in，year是取年份的

```cpp
select no,name,birthday from student where year(birthday) in (SELECT YEAR(birthday) FROM student WHERE no IN (101, 108))
```

**查询 `'张旭'` 教师任课的学生成绩表。**

首先找到教师编号：

```
SELECT NO FROM teacher WHERE NAME = '张旭'
```

通过 `sourse` 表找到该教师课程号：

```
SELECT NO FROM course WHERE t_no = ( SELECT NO FROM teacher WHERE NAME = '张旭' );
```

通过筛选出的课程号查询成绩表：

```
SELECT * FROM score WHERE c_no = (
    SELECT no FROM course WHERE t_no = ( 
        SELECT no FROM teacher WHERE NAME = '张旭' 
    )
);
```



#### 重点：union和notin的使用

找计算机系中不同职称的老师，也就是计算机系和电子工程系都有副教授，那就不要了，找独一无二的

```cpp
select * from teacher where depart='计算机系' and prof not in(select prof from teacher where depart='电子工程系')；
```

如果想把两条指令连接在一起，用一个union就可以，求并集的意思。



**查询课程 `3-105` 且成绩 至少 高于 `3-245` 的 `score` 表。**

==any关键字表示任意一个==

```cpp
SELECT * FROM score WHERE c_no = '3-105' AND degree > ANY(
    SELECT degree FROM score WHERE c_no = '3-245'
) ORDER BY degree DESC;
```

==且，所有的：all==

```cpp
xxxxxxxxxx SELECT * FROM score WHERE c_no = '3-105' AND degree > ALL(    SELECT degree FROM score WHERE c_no = '3-245') ORDER BY degree DESC;
```

![image-20230302204342362](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230302204342362.png)

**查询成绩比该课程平均成绩低的同学的成绩表：**

```cpp
select con,avg(degree) from score group by cno;
```

![image-20230302205309447](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230302205309447.png)

```cpp
select * from score a where degree < (select avg(degree) from score b where a.cno=b.cno);
```

**查询所有任课 ( 在 `course` 表里有课程 ) 教师的 `name` 和 `department`** 。

```c++
SELECT name, department FROM teacher WHERE no IN (SELECT t_no FROM course);
```

**查询 `student` 表中至少有 2 名男生的 `class` 。**

```c++
SELECT class FROM student WHERE sex = '男' GROUP BY class HAVING COUNT(*) > 1;
```

**查找不姓王的同学的记录**

==%==和linux中的*很像，表示任意的。

```cpp
select * from student where sname not like '王%'；
```

**查找student表中每个学生的姓名和年龄**

```cpp
获取当前年份
mysql> select year(now());
+-------------+
| year(now()) | 
+-------------+
|        2023 |
+-------------+ 
mysql> select name,year(now())-year(birthday) as '年龄'from student;
+-----------+--------+
| name      | 年龄   |
+-----------+--------+
| 曾华      |     46 |
| 匡明      |     48 |
| 王丽      |     47 |
| 李军      |     47 |
| 王芳      |     48 |
| 陆军      |     49 |
| 王尼玛    |     47 |
| 张全蛋    |     48 |
| 赵铁柱    |     49 |
+-----------+--------+
9 rows in set (0.04 sec)
```



**求最大最小值**

```cpp
mysql> select max(birthday) as '最大',min(birthday) as '最小'from student;
+------------+------------+
| 最大       | 最小       |
+------------+------------+
| 1977-09-01 | 1974-06-03 |
+------------+------------+
```



**按照班号和年龄从大到小的顺序查询student表中全部记录：**

按照第一个的顺序为先。

```cpp
mysql> select * from student order by class desc,birthday;
+-----+-----------+-----+------------+-------+
| no  | name      | sex | birthday   | class |
+-----+-----------+-----+------------+-------+
| 103 | 王丽      | 女  | 1976-01-23 | 95033 |
| 104 | 李军      | 男  | 1976-02-20 | 95033 |
| 107 | 王尼玛    | 男  | 1976-02-20 | 95033 |
| 101 | 曾华      | 男  | 1977-09-01 | 95033 |
| 106 | 陆军      | 男  | 1974-06-03 | 95031 |
| 109 | 赵铁柱    | 男  | 1974-06-03 | 95031 |
| 105 | 王芳      | 女  | 1975-02-10 | 95031 |
| 108 | 张全蛋    | 男  | 1975-02-10 | 95031 |
| 102 | 匡明      | 男  | 1975-10-02 | 95031 |
+-----+-----------+-----+------------+-------+
```



**查询男教师及其所上的课程**

```cppmysql> select * from course where t_no in (select no from teacher where sex='男');
+-------+--------------+------+
| no    | name         | t_no |
+-------+--------------+------+
| 3-245 | 操作系统     | 804  |
| 6-166 | 数字电路     | 856  |
+-------+--------------+------+
2 rows in set (0.00 sec)
```

**查询最高分同学的 `score` 表。**

```
select * from score where degree=(select max(degree) from score);
+------+-------+--------+
| s_no | c_no  | degree |
+------+-------+--------+
| 103  | 3-105 |     92 |
+------+-------+--------+
1 row in set (0.05 sec)
```

**查询所有选修 "计算机导论" 课程的 "男" 同学成绩表。**

```cpp
SELECT * FROM score WHERE c_no = (
    SELECT no FROM course WHERE name = '计算机导论'
) AND s_no IN (
    SELECT no FROM student WHERE sex = '男'
);
+------+-------+--------+
| s_no | c_no  | degree |
+------+-------+--------+
| 101  | 3-105 |     90 |
| 102  | 3-105 |     91 |
| 104  | 3-105 |     89 |
| 109  | 3-105 |     76 |
+------+-------+--------+
```

==**查询所有学生的 `s_no` 、`c_no` 和 `grade` 列。**==

思路是，使用区间 ( `BETWEEN` ) 查询，判断学生的成绩 ( `degree` ) 在 `grade` 表的 `low` 和 `upp` 之间

```cpp
CREATE TABLE grade (
    low INT(3),
    upp INT(3),
    grade char(1)
);

INSERT INTO grade VALUES (90, 100, 'A');
INSERT INTO grade VALUES (80, 89, 'B');
INSERT INTO grade VALUES (70, 79, 'C');
INSERT INTO grade VALUES (60, 69, 'D');
INSERT INTO grade VALUES (0, 59, 'E');

SELECT * FROM grade;
+------+------+-------+
| low  | upp  | grade |
+------+------+-------+
|   90 |  100 | A     |
|   80 |   89 | B     |
|   70 |   79 | C     |
|   60 |   69 | D     |
|    0 |   59 | E     |
+------+------+-------+
    
    
mysql> select s_no,c_no,grade from score,grade where degree between low and upp;
+------+-------+-------+
| s_no | c_no  | grade |
+------+-------+-------+
| 103  | 3-105 | A     |
| 103  | 3-245 | B     |
| 103  | 6-166 | B     |
| 105  | 3-105 | B     |
| 105  | 3-245 | C     |
| 105  | 6-166 | C     |
| 109  | 3-105 | C     |
| 109  | 3-245 | D     |
| 109  | 6-166 | B     |
+------+-------+-------+
9 rows in set (0.04 sec)
```



###SQL的四种连接查询

- 内连接
  - inner join 或者join
  - ![image-20230303153438668](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230303153438668.png)
- 外连接
  - 左连接 ：left join 或者 left outer join
  - ![image-20230303153427416](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230303153427416.png)
  - 右连接：right join 或 right outer join
  - ![image-20230303153451863](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230303153451863.png)
  - 完全外连接： full join 或 full outer join**(mysql不支持全外连接)**

创建两个表：

![image-20230303151349557](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230303151349557.png)

目前这两个表没有创建外键连接

1**.内联查询：**其实两张表中的数据没通过某个字段相等查询出相关记录

inner join查询：

==inner join连接查询，把Person中的cardId和card中的id一一对应==

用on表示条件，inner join和join是差不多的。

```cpp
select * from person inner join card on person.cardId=card.id;
+------+--------+--------+------+-----------+
| id   | name   | cardId | id   | name      |
+------+--------+--------+------+-----------+
|    1 | 张三   |      1 |    1 | 饭卡      |
|    2 | 李四   |      3 |    3 | 农行卡    |
+------+--------+--------+------+-----------+
```



**2.left join（外连接）**

左外连接会把左边表中所有数据取出来，而右边表中的数据，如果有相等的，就显示出来。没有就补上NULL

```cpp
 select * from person left join card on person.cardId=card.id;
+------+--------+--------+------+-----------+
| id   | name   | cardId | id   | name      |
+------+--------+--------+------+-----------+
|    1 | 张三   |      1 |    1 | 饭卡      |
|    2 | 李四   |      3 |    3 | 农行卡    |
|    3 | 王五   |      6 | NULL | NULL      |
+------+--------+--------+------+-----------+
```

3. **right join**

```cpp
 select * from person right join card on person.cardId=card.id;
+------+--------+--------+------+-----------+
| id   | name   | cardId | id   | name      |
+------+--------+--------+------+-----------+
|    1 | 张三   |      1 |    1 | 饭卡      |
| NULL | NULL   |   NULL |    2 | 建行卡    |
|    2 | 李四   |      3 |    3 | 农行卡    |
| NULL | NULL   |   NULL |    4 | 工商卡    |
| NULL | NULL   |   NULL |    5 | 邮政卡    |
+------+--------+--------+------+-----------+
```

4. 全连接（mysql中）

```cpp
 select * from person left join card on person.cardId=card.id
 and
 select * from person right join card on person.cardId=card.id;
```



**连接的作用在于可以不用创外键，可以通过某个值的关系来求交并集、**



### mysql事务

**-自动提交**

**-手动提交**

**-事务回滚**

在 MySQL 中，事务其实是一个最小的不可分割的工作单元。事务能够**保证一个业务的完整性**。

比如银行转账

```cpp
-- a -> -100
UPDATE user set money = money - 100 WHERE name = 'a';

-- b -> +100
UPDATE user set money = money + 100 WHERE name = 'b';
```

多条sql语句，可能会有同时成功的要求，要么就同时失败，不能只完成部分



**mysql中默认开启事务。**

```cpp
-- 查询事务的自动提交状态
SELECT @@AUTOCOMMIT;
+--------------+
| @@AUTOCOMMIT |
+--------------+
|            1 |
+--------------+
```

默认事务开启的作用：当我执行应该sql语句的时候，效果会立即体现，且不能回滚。

回滚：撤销前面语句和前面的动作

```cpp
rollback;//回滚语句 
```

通过设置mysql自动提交为false；就可以回滚

```cpp
set autocommit=0; //set autocommit=1；默认设置回去
```

然后你插入数据之后需要每次都commit一下才可以将数据真正提交.每次都手动提交。

```cpp
commit;
```



**如何手动开启一个事务：**

````cpp
begin;
start transaction;
````



直接：这样执行完就可以rollback了

```cpp
begin;
UPDATE user set money = money - 100 WHERE name = 'a';
UPDATE user set money = money + 100 WHERE name = 'b';
```

但是这样开启的事务在commit之后就结束了也就是说不能再回滚了。



**事务的特征：**

A:原子性atomic

C:一致性：事务要求同一事务中的sql语句必须保证同时成功或者同时失败

I:隔离性：事务1和事务2之间具有隔离性（也就是线程同步的问题）

D:持久性：事务一旦结束（commit），就不可以返回（rollback）。



事务开启三种方式：

```cpp
修改默认提交：set autocommit=0；
begin；
start transaction；
```



**事务的隔离性可分为四种 ( 性能从高到低 )** ：隔离级别越高性能越差

1. **READ UNCOMMITTED ( 读取未提交 )**

   如果有多个事务，那么任意事务都可以看见其他事务的**未提交数据**。

2. **READ COMMITTED ( 读取已提交 )**

   只能读取到其他事务**已经提交的数据**。

3. **REPEATABLE READ ( 可被重复读 )**

   如果有多个连接都开启了事务，那么事务之间不能共享数据记录，否则只能共享已提交的记录。

4. **SERIALIZABLE ( 串行化 )**

   所有的事务都会按照**固定顺序执行**，执行完一个事务后再继续执行下一个事务的**写入操作**。



1.read uncommitted

查看当前数据库的默认隔离级别：

```cpp
SELECT @@GLOBAL.TRANSACTION_ISOLATION;
+--------------------------------+
| @@GLOBAL.TRANSACTION_ISOLATION |
+--------------------------------+
| REPEATABLE-READ                |
+--------------------------------+
```

如何修改隔离级别？

```cpp
-- 设置系统隔离级别，LEVEL 后面表示要设置的隔离级别 (READ UNCOMMITTED)。
SET GLOBAL TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

相当于两个不同的终端同时操作，一方的操作会被另外一端的事务读取到。

未提交的这部分东西叫**脏读**

#### 脏读（uncommitted的情况下就会出现脏读）

测试 **READ UNCOMMITTED ( 读取未提交 )** 的隔离性：

```
INSERT INTO user VALUES (3, '小明', 1000);
INSERT INTO user VALUES (4, '淘宝店', 1000);

SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |  1000 |
|  4 | 淘宝店    |  1000 |
+----+-----------+-------+

-- 开启一个事务操作数据
-- 假设小明在淘宝店买了一双800块钱的鞋子：
START TRANSACTION;
UPDATE user SET money = money - 800 WHERE name = '小明';
UPDATE user SET money = money + 800 WHERE name = '淘宝店';

-- 然后淘宝店在另一方查询结果，发现钱已到账。
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |   200 |
|  4 | 淘宝店    |  1800 |
+----+-----------+-------+
```

由于小明的转账是在新开启的事务上进行操作的，而该操作的结果是可以被其他事务（另一方的淘宝店）看见的，因此淘宝店的查询结果是正确的，淘宝店确认到账。但就在这时，如果小明在它所处的事务上又执行了 `ROLLBACK` 命令，会发生什么？

```
-- 小明所处的事务
ROLLBACK;

-- 此时无论对方是谁，如果再去查询结果就会发现：
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |  1000 |
|  4 | 淘宝店    |  1000 |
+----+-----------+-------+
```

这就是所谓的**脏读**，**一个事务读取到另外一个事务还未提交的数据。**这在实际开发中是不允许出现的。



2.读到已经提交的事务**READ COMMITTED ( 读取已提交 )**

#### 读取已提交

把隔离级别设置为 **READ COMMITTED** ：

```
SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED;
SELECT @@GLOBAL.TRANSACTION_ISOLATION;
+--------------------------------+
| @@GLOBAL.TRANSACTION_ISOLATION |
+--------------------------------+
| READ-COMMITTED                 |
+--------------------------------+
```

这样，再有新的事务连接进来时，它们就只能查询到已经提交过的事务数据了。但是对于当前事务来说，它们看到的还是未提交的数据，例如：

```
-- 正在操作数据事务（当前事务）
START TRANSACTION;
UPDATE user SET money = money - 800 WHERE name = '小明';
UPDATE user SET money = money + 800 WHERE name = '淘宝店';

-- 虽然隔离级别被设置为了 READ COMMITTED，但在当前事务中，
-- 它看到的仍然是数据表中临时改变数据，而不是真正提交过的数据。
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |   200 |
|  4 | 淘宝店    |  1800 |
+----+-----------+-------+


-- 假设此时在远程开启了一个新事务，连接到数据库。
$ mysql -u root -p12345612

-- 此时远程连接查询到的数据只能是已经提交过的
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |  1000 |
|  4 | 淘宝店    |  1000 |
+----+-----------+-------+
```

但是这样还有问题，那就是假设一个事务在操作数据时，其他事务干扰了这个事务的数据。例如：

```
-- 小张在查询数据的时候发现：
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |   200 |
|  4 | 淘宝店    |  1800 |
+----+-----------+-------+

-- 在小张求表的 money 平均值之前，小王做了一个操作：
START TRANSACTION;
INSERT INTO user VALUES (5, 'c', 100);
COMMIT;

-- 此时表的真实数据是：
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |  1000 |
|  4 | 淘宝店    |  1000 |
|  5 | c         |   100 |
+----+-----------+-------+

-- 这时小张再求平均值的时候，就会出现计算不相符合的情况：
SELECT AVG(money) FROM user;
+------------+
| AVG(money) |
+------------+
|  820.0000  |
+------------+
```

虽然 **READ COMMITTED** 让我们只能读取到其他事务已经提交的数据，但还是会出现问题，就是**在读取同一个表的数据时，可能会发生前后不一致的情况。\**这被称为\**不可重复读现象 ( READ COMMITTED )** 。



####幻读

将隔离级别设置为 **REPEATABLE READ ( 可被重复读取 )** :

```
SET GLOBAL TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SELECT @@GLOBAL.TRANSACTION_ISOLATION;
+--------------------------------+
| @@GLOBAL.TRANSACTION_ISOLATION |
+--------------------------------+
| REPEATABLE-READ                |
+--------------------------------+
```

测试 **REPEATABLE READ** ，假设在两个不同的连接上分别执行 `START TRANSACTION` :

```
-- 小张 - 成都
START TRANSACTION;
INSERT INTO user VALUES (6, 'd', 1000);

-- 小王 - 北京
START TRANSACTION;

-- 小张 - 成都
COMMIT;
```

当前事务开启后，没提交之前，查询不到，提交后可以被查询到。但是，在提交之前其他事务被开启了，那么在这条事务线上，就不会查询到当前有操作事务的连接。相当于开辟出一条单独的线程。

无论小张是否执行过 `COMMIT` ，在小王这边，都不会查询到小张的事务记录，而是只会查询到自己所处事务的记录：

```
SELECT * FROM user;
+----+-----------+-------+
| id | name      | money |
+----+-----------+-------+
|  1 | a         |   900 |
|  2 | b         |  1100 |
|  3 | 小明      |  1000 |
|  4 | 淘宝店    |  1000 |
|  5 | c         |   100 |
+----+-----------+-------+
```

这是**因为小王在此之前开启了一个新的事务 ( `START TRANSACTION` ) \**，那么\**在他的这条新事务的线上，跟其他事务是没有联系的**，也就是说，此时如果其他事务正在操作数据，它是不知道的。

然而事实是，在真实的数据表中，小张已经插入了一条数据。但是小王此时并不知道，也插入了同一条数据，会发生什么呢？

```
INSERT INTO user VALUES (6, 'd', 1000);
-- ERROR 1062 (23000): Duplicate entry '6' for key 'PRIMARY'
```

报错了，操作被告知已存在主键为 `6` 的字段。这种现象也被称为**幻读，一个事务提交的数据，不能被其他事务读取到**。

#### 串行化

顾名思义，就是所有事务的**写入操作**全都是串行化的。什么意思？把隔离级别修改成 **SERIALIZABLE** :

```
SET GLOBAL TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SELECT @@GLOBAL.TRANSACTION_ISOLATION;
+--------------------------------+
| @@GLOBAL.TRANSACTION_ISOLATION |
+--------------------------------+
| SERIALIZABLE                   |
+--------------------------------+
```

此时会发生什么呢？由于现在的隔离级别是 **SERIALIZABLE ( 串行化 )** ，串行化的意思就是：假设把所有的事务都放在一个串行的队列中，那么所有的事务都会按照**固定顺序执行**，执行完一个事务后再继续执行下一个事务的**写入操作** ( **这意味着队列中同时只能执行一个事务的写入操作** ) 。

根据这个解释，小王在插入数据时，会出现等待状态，直到小张执行 `COMMIT` 结束它所处的事务，或者出现等待超时。

**相当于读写锁。**





## 2.如何使用可视化工具操作数据库



## 3.如何在编程语言中操作数据库



