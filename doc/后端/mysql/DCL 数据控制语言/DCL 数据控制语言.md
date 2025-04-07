# DCL 数据控制语言

## 目录

- [管理用户](#管理用户)
- [权限](#权限)
  - [权限](#权限)

> 管理数据库 用户，访问权限。&#x20;

## 管理用户

```sql 
# 查询用户
use mysql ;
select * from user;

# 创建用户
create user '用户名'@'主机名' identified by '密码';
# 任意主机
create user '用户名'@'%' identified by '密码';


# 修改用户
alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';

# 删除用户
drop user '用户名'@'主机名';



```


## 权限

```sql 
# 查询权限
show grants for '用户名'@'主机名';

# 授予权限
grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';
# 授予所有数据库表的权限给用户
grant all on *.* to '用户名'@'主机名';

# 撤销权限
revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';

```


### 权限

| all，all privileges | 所有权限       |
| ------------------ | ---------- |
| selcet             | 查询         |
| insert             | 插入数据       |
| update             | 更新数据       |
| delete             | 删除数据       |
| alter              | 修改表        |
| drop               | 删除数据库/表/视图 |
| create             | 创建数据库/表    |
