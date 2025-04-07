# DDL 数据定义语言

## 目录

- [数据库](#数据库)
- [表](#表)
- [示例](#示例)
  - [创建表](#创建表)
    - [示例](#示例)

# 数据库

```bash 
// 创建数据库
create database [if not exists] 数据库名;

// 删除数据库
drop database [if exists] 数据库名;

// 使用数据库
use 数据库名;


```


# 表

```sql 
# 创建表
create table [if not exists ] 表名(
    字段1 类型 [其他约束 primary key | auto_increment | not null | default '' ] [comment '主键'],
    字段2 类型 [comment '名称'],
    字段3 类型 comment '备注'
)[comment '测试表'];

# 添加字段
alter table 表名 add 字段名 类型 [comment '注释'][约束];

# 修改数据类型
alter table 表名 modify 字段名 新数据类型;

# 修改字段名和字段类型
alter table 表名 change 旧字段名 新字段名 类型 [comment '注释'][约束];

# 删除字段
alter table 表名 drop 字段名;

# 修改表名
alter table 旧表名 rename to 新表名

# 删除表
drop table [if exists] 表名;

# 会把id等一些信息重置
truncate table 表名;


```


1. create database : 创建新数据库
2. alter  database : 修改数据库
3. craete table : 创建表
4. alter table <表名> \<change|modify|drop (动作)> <字段名> : 改变数据库
5. drop table ： 删除表
6. create index : 创建索引
7. drop index : 删除索引

&#x20;

# 示例

## 创建表

```sql 
create table if not exists my_test(
    id bigint primary key  auto_increment comment '主键',
    name varchar(50) not null default '' comment '名称',
    remark text not null comment '备注'
)comment '测试表'


# 创建员工表
create table if not exists emp
(
    id         int primary key auto_increment not null comment '主键id',
    work_no    varchar(10)                    not null default '' comment '工号',
    name       varchar(10)                    not null default '' comment '员工姓名',
    gender     char(1)                        not null default '' comment '性别',
    age        tinyint unsigned               not null default 1 comment '年龄',
    id_card    char(18)                       not null default '' comment '身份证',
    entry_date date comment '入职时间'
) comment '员工表'




```


```sql 
## 修改表字段
alter table tableName 
change <旧字段名> <新字段名> <新数据类型>


## 新增索引
create <unique(唯一索引)> index table_colu_name
on tableName (column1,column2)



```


#### 示例

```sql 
select <distinct><top> <字段>
from 表名 <别名>
Where 条件
Group By 字段
Having 条件
Order By 字段
Limit skipNum ,takeNum

```
