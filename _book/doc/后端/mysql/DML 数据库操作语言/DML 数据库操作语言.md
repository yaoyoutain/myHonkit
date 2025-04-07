# DML 数据库操作语言

## 目录

- [其他复杂的操作语句](#其他复杂的操作语句)

1. select
2. insert into&#x20;
3. update
4. delete

```sql 
# 添加数据
insert into 表名(字段名1,字段名2,字段名3) values(val1,val2,val3)
insert into 表名 values(val1,val2,val3)

# 批量新增
insert into 表名(字段名1,字段名2,字段名3) values(val1,val2,val3),(val1,val2,val3)
insert into 表名 values(val1,val2,val3),(val1,val2,val3),(val1,val2,val3)

# 更新
update 表名 set 字段名1=val1, 字段名2=val2 
[where 条件];

# 删除
delete from 表名 
[where 条件];





```


#### 其他复杂的操作语句

1. insert select : 根据查询新增
   ```sql 
   INSERT INTO table2 (column1, column2, column3, ...)
   SELECT column1, column2, column3, ...
   FROM table1
   WHERE condition;
   ```

2. udpate : 多表更新
   ```sql 
   update table1,table2
   set table1.col1 = table2.col1,
   table1.col2 = table2.col2
   where table1.id=table2.id
   ```
