
# SQL 基本操作

## CURD 增删改查

> 它代表创建（Create）、更新（Update）、读取（Retrieve）和删除（Delete）操作。

## 库操作

#### 增

`create database + 数据库名称 + [库选项]`
库选项:

-   字符集设定
-   校对集设定
    -   `_bin`：binary，二进制比较，取出二进制位，一位一位进行比较，区分大小写；
    -   `_cs`：case sensitive，大小写敏感，区分大小写；
    -   `_ci`：case insensitive，大小写不敏感，不区分大小写。

```sql
create database db1 charset utf8
```

#### 删

`drop database + 数据库名称;`

#### 改

`alter database + 数据库名称 + [库选项];`
库选项

-   charset/character set[=] 字符集;
-   collate[=] 校对集;

```sql
alter database TBL_ERROR_CODE charset gbk
```

**_数据库的名字不可以修改_**

#### 查

`show databases;`

`show databases like 'pattern';`

> `%`：表示匹配多个字符；

```sql
show databases like 'TBL%';
```

`show create database + 数据库名称;`

```sql
show create database user
```

## 表操作

#### 增

```
create table [if not exists] + 表名(
    字段名称 数据类型 [列属性/字段属性],
    ……
    字段名称 数据类型   /* 最后后一行，不需要加逗号 */
)[表选项];
```

```sql
CREATE TABLE `student` (
  `student_id` int(11) NOT NULL AUTO_INCREMENT,
  `student_name` varchar(255) NOT NULL,
  `student_sex` tinyint(1) NOT NULL COMMENT '0 for girl 1 for boy',
  `student_score` int(11) NOT NULL DEFAULT '0' COMMENT '学生分数',
  PRIMARY KEY (`student_id`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8 ROW_FORMAT=COMPACT;
```

**表选项**

-   字符集设定：charset/ character set+ 具体字符集，用来表示数据存储的编码格式，常用的字符集包括 GBK 和 UTF8 等。
-   校对集设定：collate+ 具体校对集，表示数据比较的规则，其依赖字符集。
-   存储引擎：engine+具体存储引擎，默认为 InnoDB，常用的还有 MyISAM.

**表名**

-   任何表都归属于某个数据库，因此在创建表的时候，都必须先指定具体的数据库

显示

```sql
create table if not exists test.student(
    name varchar(10),
    age int,            /* 整型不需要指定具体的长度 */
    grade varchar(10)   /* 最后后一行，不需要加逗号 */
)charset utf8;
```

隐式

```sql
use test;               /* use + 数据库名称，表示切换到指定的数据库，这句命令其实不加分号也可以，但不建议这么做 */
create table if not exists student(
    name varchar(10),
    age int,            /* 整型不需要指定具体的长度 */
    grade varchar(10)   /* 最后后一行，不需要加逗号 */
)charset utf8;
```

#### 删

删一个
`drop table + 表1`
删多个
`drop table + 表1, 表2 ...`

#### 改

-   修改表名，基本语法：`rename table 旧表名 to 新表名;`
-   修改表选项，基本语法：`alter table + 表名 + 表选项[=] + 值;`

#### 查

```sql
show tables;
```

`show tables like 'pattern';`
%：表示匹配多个字符；

```sql
show tables like '%t';
```

`show create table + 表名;`

`desc/describe/show columns from + 表名;`

## 字段操作

#### 增

`alter table + 表名 + add + [column] + 字段名 + 数据类型 + [列属性][位置];`

`位置表示此字段存储的位置，分为first（第一个位置）和after + 字段名（指定的字段后，默认为最后一个位置）`

```sql
alter table student add column id int first;`
```

#### 删

`alter table + 表名 + drop+ 字段名;`

```sql
alter table student drop age;
```

> 如果已存在数据,会清空数据

#### 改

`alter table + 表名 + modify + 字段名 + 数据类型 + [列属性][位置];`

```sql
alter table student modify name char(10) after id;
```

`alter table + 表名 + change + 旧字段名 + 新字段名 + 数据类型 + [列属性][位置];`

```sql
alter table student change grade class varchar(10);
```

#### 查

`show create table + 表名;`

# 列/字段类型

## 数值型

#### 整数

-   tinyint：迷你整型，使用 1 个字节存储数据（常用）；
-   smallint：小整型，使用 2 个字节存储数据；
-   mediumint：中整型，使用 3 个字节存储数据；
-   int：标准整型，使用 4 个字节存储数据（常用）；
-   bigint：大整型，使用 8 个字节存储数据。

#### 小数

-   float：单精度，占用 4 个字节存储数据，精度范围大概为 7 位左右；
-   double：双精度，占用 8 个字节存储数据，精度范围大概为 15 位左右。
-   如果直接用 float，则表示没有小数部分；
-   如果用 float(M,D)，其中 M 代表总长度，D 代表小数部分长度，M-D 则为整数部分长度。

## 日期时间型

-   datetime：日期时间，其格式为 yyyy-MM-dd HH:mm:ss，表示的范围是从 1000 年到 9999 年，有零值，即 0000-00-00 0000:00；
-   date：日期，就是 datetime 的 date 部分；
-   time：时间，或者说是时间段，为指定的某个时间区间之间，包含正负时间；
-   timestamp：时间戳，但并不是真正意义上的时间戳，其是从 1970 年开始计算的，格式和 datetime 一致；支持自动更新
-   year：年份，共有两种格式，分别为 year(2)和 year(4).

## 字符串型

#### 定长字符串

-   在定义结构的时候就已经确定了最终数据的存储长度。
-   char(L)：L 表示 Length，即可以存储的长度，单位为字符，最大长度为 255；
-   char(4)：表示在 UTF8 环境下，需要 4\*3=12 个字节。

#### 变长字符串

-   varchar，即在分配存储空间的时候，按照最大的空间分配，但是实际用了多少，则是根据具体的数据来确定。
-   varchar(L)：L 表示 Length，理论长度是 65536，但是会多出 1 到 2 个字节来确定存储的实际长度；

> varchar(10)：例如存储 10 个汉字，在 UTF8 环境下，需要 10\*3+1=31 个字节。

如何选择定长字符串或者是变长字符串呢？

-   定长字符串对磁盘空间比较浪费，但是效率高：如果数据基本上确定长度都一样，就使用定长字符串，例如身份证、电话号码等；
-   变长字符串对磁盘空间比较节省，但是效率低：如果数据不能确定长度（不同的数据有变化），就使用变长字符串，例如地址、姓名等。

#### 文本字符串

-   如果数据量非常大，通常说超过 255 个字符就会使用文本字符串。
-   文本字符串根据存储的格式进行分类，可以分为：
    -   text：存储文字；
    -   blob：存储二进制数据（其实际上都是存储路径），通常不用。

#### 枚举字符串

-   enum，需要事先将所有可能出现的结果都设计好，实际上存储的数据必须是规定好的数据中的一个。
-   枚举字符串的使用方式：
    -   定义：enum('元素 1','元素 2','元素 3'...)，例如 enum('男','女','保密')；
    -   使用：存储的数据，只能是事先定义好的数据。

#### 集合字符串

-   set，跟枚举类似，实际存储的是数值而不是字符串。

集合字符串的使用方式：

_ 定义：set，元素列表；
_ 使用：可以使用元素列表中的多个元素，用逗号分隔。

# 列属性

## null

空属性

## not null

非空属性

## default

默认值

## primary key

主键

> 主键对应的字符中的数据不允许重复，如果重复，则数据操作（主要是增和改）失败

## unique key

唯一键

> 当唯一键满足非空条件的时候，其性质就和主键一样

## auto_increment

自增

> 当对应的字段，不给值/null, 系统会从当前字段中取已有的最大值再进行+1 操作，得到新的字段值
> 主键一般是递增的
> 自增长字段必须是数字（整型）；
> 每张表最多有一个自增长字段。

## comment

备注/注释

# 关系

## 一对一(1:1)

「个人信息表」，其字段包含：姓名、性别、年龄、身高、体重、籍贯和居住地等

## 一对多/多对一(1:N/N:1)

国家表,城市表

## 多对多(N:N)

学生表, 课程表

> 需要中间表建立联系

# 范式

## 简介

#### 什么是范式

> 设计数据表遵守的规范

#### 意义何在?

> 是为了解决数据的存储和优化问题

## 特点

-   非必须
-   越来越严格
-   向下兼容

## 内容

-   数据表中的每一列（每个字段）必须是不可拆分的最小单元，也就是确保每一列的原子性
-   满足 1NF 后，要求表中的所有列，都必须依赖于主键，而不能有任何一列与主键没有关系
-   必须先满足第二范式（2NF），要求：表中的每一列只与主键直接相关而不是间接相关

## 说人话

-   一个字段只存一个数据
-   一张表只干一件事
-   不属于这个表的字段, 不要加到这个表里来

![img](images/1118686-20170616134418946-1189742758.png)

![img](images/1118686-20170616134438775-1068700526.png)

![img](images/1118686-20170616134457821-1631705781.png)

## 逆规范化

冗余和效率

# 数据操作(增)

## SQL INSERT INTO 语句

INSERT INTO 语句用于向表中插入新记录。

### SQL INSERT INTO 语法

INSERT INTO 语句可以有两种编写形式。

第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

```sql
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```

第二种形式需要指定列名及被插入的值：

```sql
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

```sql
INSERT INTO Websites (name, url, alexa, country) VALUES ('百度','https://www.baidu.com/','4','CN');
```

## 在指定的列插入数据

我们也可以在指定的列插入数据。

## 实例

```sql
INSERT INTO Websites (name, url, country) VALUES ('stackoverflow', 'http://stackoverflow.com/', 'IND');
```

# 数据操作(删)

## SQL DELETE 语句

DELETE 语句用于删除表中的行。

### SQL DELETE 语法

```sql
DELETE FROM table_name WHERE some_column=some_value;
```

**请注意 SQL DELETE 语句中的 WHERE 子句！**

> WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！ |

## SQL DELETE 实例

假设我们要从 "Websites" 表中删除网站名为 "百度" 且国家为 CN 的网站 。

我们使用下面的 SQL 语句：

## 实例

```sql
DELETE FROM Websites WHERE name='百度' AND country='CN';
```

## 删除所有数据

您可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

```sql
DELETE FROM table_name;
DELETE * FROM table_name;
```

**注释：** 在删除记录时要格外小心！因为不能重来！

# 数据操作(改)

## SQL UPDATE 语句

UPDATE 语句用于更新表中已存在的记录。

### SQL UPDATE 语法

```sql
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```

| ![lamp](images/lamp-1546381164742.jpg) | **请注意 SQL UPDATE 语句中的 WHERE 子句！** WHERE 子句规定哪条记录或者哪些记录需要更新。如果您省略了 WHERE 子句，所有的记录都将被更新！ |

## SQL UPDATE 实例

假设我们要把 "sql 教程" 的 rank 排名更新为 5000，country 改为 USA。

我们使用下面的 SQL 语句：

## 实例

```sql
UPDATE Websites  SET rank='5000', country='USA'  WHERE name='sql教程';
```

## Update 警告！

在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

`UPDATE Websites SET rank='5000', country='USA'`

执行以上代码会将 数据表中所有数据的 rank 改为 5000，country 改为 USA。

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。

# 数据操作(查)

## SQL SELECT 语句

> SELECT 语句用于从数据库中选取数据。

结果被存储在一个结果表中，称为结果集。

#### SQL SELECT 语法

```sql
SELECT column_name,column_name FROM table_name;
```

```sql
SELECT * FROM table_name;
```

## SQL SELECT DISTINCT 语句

> 在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。

DISTINCT 关键词用于返回唯一不同的值。

SQL SELECT DISTINCT 语法

```sql
SELECT DISTINCT column_name,column_name FROM table_name;
```

## SQL WHERE 子句

> WHERE 子句用于提取那些满足指定标准的记录。

## SQL WHERE 语法

```sql
SELECT column_name,column_name FROM table_name WHERE column_name operator value;
```

文本和数值

```sql
SELECT * FROM Websites WHERE country='CN';
```

```sql
SELECT * FROM Websites WHERE id=1;
```





## WHERE 子句中的运算符

下面的运算符可以在 WHERE 子句中使用：

| 运算符  | 描述                                                       |
| ------- | ---------------------------------------------------------- |
| =       | 等于                                                       |
| <>      | 不等于。**注释：**在 SQL 的一些版本中，该操作符可被写成 != |
| >       | 大于                                                       |
| <       | 小于                                                       |
| >=      | 大于等于                                                   |
| <=      | 小于等于                                                   |
| BETWEEN | 在某个范围内                                               |
| LIKE    | 搜索某种模式                                               |
| IN      | 指定针对某个列的多个可能值                                 |

## SQL AND & OR 运算符

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。



## 结合 AND & OR

您也可以把 AND 和 OR 结合起来（使用圆括号来组成复杂的表达式）。

下面的 SQL 语句从 "Websites" 表中选取 alexa 排名大于 "15" 且国家为 "CN" 或 "USA" 的所有网站：

## 实例

```sql
SELECT * FROM Websites WHERE rank > 15 AND (country='CN' OR country='USA');
```





## SQL ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

### SQL ORDER BY 语法

```sql
SELECT column_name,column_name
FROM table_name
ORDER BY column_name,column_name ASC|DESC;
```



## MySQL SELECT LIMIT 实例



返回几条



```sql
SELECT * FROM Websites LIMIT 2;
```

## SQL LIKE 操作符

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

### SQL LIKE 语法

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```



not like 取反

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name NOT LIKE pattern;
```



## IN 操作符

IN 操作符允许您在 WHERE 子句中规定多个值。

### SQL IN 语法

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...);
```



## SQL BETWEEN 操作符

BETWEEN 操作符选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

### SQL BETWEEN 语法

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```



## NOT BETWEEN 操作符(取反)



```sql
SELECT column_name(s)
FROM table_name
WHERE column_name NOT BETWEEN value1 AND value2;
```



## SQL 别名

通过使用 SQL，可以为表名称或列名称指定别名。

基本上，创建别名是为了让列名称的可读性更强。

### 列的 SQL 别名语法

```sql
SELECT column_name AS alias_name
FROM table_name;
```



### 表的 SQL 别名语法

```sql
SELECT column_name(s)
FROM table_name AS alias_name;
```





## SQL JOIN

SQL JOIN 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。

最常见的 JOIN 类型：**SQL INNER JOIN（简单的 JOIN）**。 SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行。

```sql
SELECT Websites.id, Websites.name, access_log.count, access_log.date
FROM Websites
INNER JOIN access_log
ON Websites.id=access_log.site_id;
```

## 不同的 SQL JOIN

* **INNER JOIN**：如果表中有至少一个匹配，则返回行
* **LEFT JOIN**：即使右表中没有匹配，也从左表返回所有的行
* **RIGHT JOIN**：即使左表中没有匹配，也从右表返回所有的行
* **FULL JOIN**：只要其中一个表中存在匹配，则返回行

> 左连接与右连接的左右指的是以两张表中的哪一张为基准，它们都是外连接。

## SQL INNER JOIN 关键字

INNER JOIN 关键字在表中存在至少一个匹配时返回行。

### SQL INNER JOIN 语法

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;
```





或：

```sql
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```





**注释：**INNER JOIN 与 JOIN 是相同的。

![SQL INNER JOIN](images/img_innerjoin.gif)



## SQL LEFT JOIN 关键字

LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

### SQL LEFT JOIN 语法

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;
```





或：

```sql
SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```





**注释：**在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。

![SQL LEFT JOIN](images/img_leftjoin.gif)





## SQL RIGHT JOIN 关键字

RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

### SQL RIGHT JOIN 语法

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name=table2.column_name;
```





或：

```sql
SELECT column_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```





**注释：**在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。

![SQL RIGHT JOIN](images/img_rightjoin.gif)



## SQL FULL OUTER JOIN 关键字

FULL OUTER JOIN 关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.

FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。

### SQL FULL OUTER JOIN 语法

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name=table2.column_name;
```





![SQL FULL OUTER JOIN](images/img_fulljoin.gif)





## AVG() 函数

AVG() 函数返回数值列的平均值。

### SQL AVG() 语法

```sql
SELECT AVG(column_name) FROM table_name
```



## MIN() 函数

MIN() 函数返回指定列的最小值。

### SQL MIN() 语法

```sql
SELECT MIN(column_name) FROM table_name;
```







## MAX() 函数

MAX() 函数返回指定列的最大值。

### SQL MAX() 语法

```sql
SELECT MAX(column_name) FROM table_name;
```



