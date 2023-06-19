# 任务重点:
* 在电脑上安装MySQL数据库系统
* 安装客户端并连接到本机上的MySQL数据库


安装数据库网上教程繁多，根据自己想要安装的数据库对应版本然后根据教程安装即可
下面是一个比较详细的安装教程
* MySQL 8.0 的安装及连接(https://github.com/datawhalechina/wonderful-sql/blob/main/ch00:%20%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA.md#1-mysql-80-%E7%9A%84%E5%AE%89%E8%A3%85)

# 1.1 初识数据库

数据库是将大量数据保存起来，通过计算机加工而成的可以进行高效访问的数据集合。该数据集合称为数据库（Database，DB）。用来管理数据库的计算机系统称为数据库管理系统（Database Management System，DBMS）。
### 1.1.1 DBMS的种类

DBMS 主要通过数据的保存格式（数据库的种类）来进行分类，现阶段主要有以下 5 种类型.

- 层次数据库（Hierarchical Database，HDB）

- 关系数据库（Relational Database，RDB）

    - Oracle Database：甲骨文公司的RDBMS
    - SQL Server：微软公司的RDBMS
    - DB2：IBM公司的RDBMS
    - PostgreSQL：开源的RDBMS
    - MySQL：开源的RDBMS

    如上是5种具有代表性的RDBMS，其特点是由行和列组成的二维表来管理数据，这种类型的 DBMS 称为关系数据库管理系统（Relational Database Management System，RDBMS）。
    
- 面向对象数据库（Object Oriented Database，OODB）

- XML数据库（XML Database，XMLDB）

- 键值存储系统（Key-Value Store，KVS），举例：MongoDB

# 1.2 初识 SQL

根据对 RDBMS 赋予的指令种类的不同，SQL 语句可以分为以下三类.

- **DDL** ：DDL（Data Definition Language，数据定义语言） 用来创建或者删除存储数据用的数据库以及数据库中的表等对象。DDL 包含以下几种指令。

    - CREATE ： 创建数据库和表等对象
    - DROP ： 删除数据库和表等对象
    - ALTER ： 修改数据库和表等对象的结构

- **DML** :DML（Data Manipulation Language，数据操纵语言） 用来查询或者变更表中的记录。DML 包含以下几种指令。

    - SELECT ：查询表中的数据
    - INSERT ：向表中插入新数据
    - UPDATE ：更新表中的数据
    - DELETE ：删除表中的数据

- **DCL** ：DCL（Data Control Language，数据控制语言） 用来确认或者取消对数据库中的数据进行的变更。除此之外，还可以对 RDBMS 的用户是否有权限操作数据库中的对象（数据库表等）进行设定。DCL 包含以下几种指令。

    - COMMIT ： 确认对数据库中的数据进行的变更
    - ROLLBACK ： 取消对数据库中的数据进行的变更
    - GRANT ： 赋予用户操作权限
    - REVOKE ： 取消用户的操作权限
### 1.2.2 数据库的创建（ CREATE DATABASE 语句）

语法：

```sql
CREATE DATABASE < 数据库名称 > ;
```
创建数据库
```sql
CREATE DATABASE shop;
```
### 1.2.3 表的创建（ CREATE TABLE 语句）

语法：

```sql
CREATE TABLE < 表名 >
( < 列名 1> < 数据类型 > < 该列所需约束 > ,
  < 列名 2> < 数据类型 > < 该列所需约束 > ,
  < 列名 3> < 数据类型 > < 该列所需约束 > ,
  < 列名 4> < 数据类型 > < 该列所需约束 > ,
  .
  .
  .
  < 该表的约束 1> , < 该表的约束 2> ,……);
```
创建商品表

```sql
CREATE TABLE product
(product_id CHAR(4) NOT NULL,
 product_name VARCHAR(100) NOT NULL,
 product_type VARCHAR(32) NOT NULL,
 sale_price INTEGER ,
 purchase_price INTEGER ,
 regist_date DATE ,
 PRIMARY KEY (product_id));
```

### 1.2.4 命名规则

* 只能使用半角英文字母、数字、下划线（_）作为数据库、表和列的名称
* 名称必须以半角英文字母开头

### 1.2.5 数据类型的指定

数据库创建的表，所有的列都必须指定数据类型，每一列都不能存储与该列数据类型不符的数据。

四种最基本的数据类型

* INTEGER 型

用来指定存储整数的列的数据类型（数字型），不能存储小数。



* CHAR 型

用来存储定长字符串，当列中存储的字符串长度达不到最大长度的时候，使用半角空格进行补足，由于会浪费存储空间，所以一般不使用。

* VARCHAR 型

用来存储可变长度字符串，定长字符串在字符数未达到最大长度时会用半角空格补足，但可变长字符串不同，即使字符数未达到最大长度，也不会用半角空格补足。

* DATE 型

用来指定存储日期（年月日）的列的数据类型（日期型）。

### 1.2.6 约束的设置

约束是除了数据类型之外，对列中存储的数据进行限制或者追加条件的功能。

`NOT NULL`是非空约束，即该列必须输入数据。

`PRIMARY KEY`是主键约束，代表该列是唯一值，可以通过该列取出特定的行的数据。

### 1.2.7 表的删除和更新

* 删除表的语法：
```sql
DROP TABLE < 表名 > ;
```
* 删除 product 表

需要特别注意的是，删除的表是无法恢复的，只能重新插入，请执行删除操作时要特别谨慎。

```sql
DROP TABLE product;
```
- 添加列的 ALTER TABLE 语句

```sql
ALTER TABLE < 表名 > ADD COLUMN < 列的定义 >;
```
- 添加一列可以存储100位的可变长字符串的 product_name_pinyin 列

```sql
ALTER TABLE product ADD COLUMN product_name_pinyin VARCHAR(100);
```
- 删除列的 ALTER TABLE 语句

```sql
ALTER TABLE < 表名 > DROP COLUMN < 列名 >;
```
- 删除 product_name_pinyin 列

```sql
ALTER TABLE product DROP COLUMN product_name_pinyin;
```
- 删除表中特定的行（语法）

```sql
-- 一定注意添加 WHERE 条件，否则将会删除所有的数据
DELETE FROM product WHERE COLUMN_NAME='XXX';
```
ALTER TABLE 语句和 DROP TABLE 语句一样，执行之后无法恢复。误添加的列可以通过 ALTER TABLE 语句删除，或者将表全部删除之后重新再创建。
