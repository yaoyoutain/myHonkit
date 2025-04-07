# database

## 目录

- [功能](#功能)
  - [前置条件](#前置条件)
  - [链接数据库](#链接数据库)
    - [知识点 ：](#知识点-)
  - [执行sql](#执行sql)
    - [知识点](#知识点)
- [单个查询](#单个查询)
  - [知识点](#知识点)
- [多个查询](#多个查询)
  - [知识点](#知识点)
- [sql复用语法Prepare](#sql复用语法Prepare)
- [事务](#事务)
  - [知识点](#知识点)

## 功能

1. 链接数据库
   1. ping
   2. 数据库链接池设置
      1. 最大链接数量
      2. 空闲时最大链接数量
2. 单个查询
3. 多个查询
4. 执行sql
   1. 新增，更新， 删除
5. sql复用语法
6. 事务

### 前置条件

```sql 
create table student(
    id bigint primary key auto_increment not null comment '主键',
    name varchar(50) default '' not null comment '名称',
    age int default 0 not null comment '年龄'
)
```


### 链接数据库

> 这里我们采用链接mysql数据库

```纯文本 
import (
  "database/sql" //导入官方包

  _ "github.com/go-sql-driver/mysql" //加载mysql 驱动
)
```


#### 知识点 ：

1. mysql dns 链接字符串: dns:= "root:123456\@tcp(127.0.0.1:3306)/test\_db"
   > 账号：密码@tcp（ip：端口）/链接数据库名称
2. sql.Open
   > 创建链接结构体sql.Open("数据库名称（mysql）",dns)
3. sqlDb.SetConnMaxLifetime
   > 设置最大活动链接数量
4. sqlDb.SetConnMaxIdleTime
   > 设置最大空闲链接数量
5. sqlDb.ping()
   > 真正链接数据

```go 

var sqlDb *sql.DB

const dns = "root:123456@tcp(127.0.0.1:3306)/test_db"

func init() {
  var err error
  // 创建sql链接数据结构：这里并没有真正的 链接
  // 这里为啥要单独声明err呢， 如果这里不单独申明的话
  // 下面就会用： 来进行赋值， 这样sqldb就是个包的局部变量
  sqlDb, err = sql.Open("mysql", dns)

  if err != nil {
    log.Fatalln("创建mysql配置错误，", err)
  }

  // 这里我们第一次ping 链接数据
  if err = sqlDb.Ping(); err != nil {
    log.Fatalln("mysql数据库链接失败，", err)
  }
  log.Println("mysql数据库链接成功dns=", dns)

  // 设置最大活动链接数量
  sqlDb.SetConnMaxLifetime(100)
  // 设置最大空闲链接数量
  sqlDb.SetConnMaxIdleTime(10)

}

```


### 执行sql

> 这个操作可以实现： 新增， 修改， 删除功能

```go 
func (s *student) Insert() (err error) {
  // 执行sql语句
  sqlResult, err := sqlDb.Exec("insert into student (name, age) values (?,?);", s.Name, s.Age)
  if err != nil {
    return
  }

  // 获取最新id
  s.Id, err = sqlResult.LastInsertId()
  if err != nil {
    return
  }

  // 获取影响行数
  rowNum, err := sqlResult.RowsAffected()
  log.Println("新增影响行数rowNum=", rowNum)
  return
}

```


#### 知识点

1. sqlDb.Exec(sqlstr)： 执行sql
2. sqlResult.LastInsertId() ： 获取最新id
3. sqlResult.RowsAffected()： 获取影响行数
4. 占位符： mysql: ？

## 单个查询

> 查询单个对象

```go 
// QueryStudentById 根据id查询
func (s *student) QueryStudentById() (err error) {
  sqlStr := "select id, name, age from student where id=?"
  // 查询单行
  row := sqlDb.QueryRow(sqlStr, s.Id)
  s = new(student)
  // 映射到结构体上， 这里需要指针地址
  err = row.Scan(&s.Id, &s.Name, &s.Age)
  return
}

```


#### 知识点

1. sqlDb.QueryRow(sqlStr, args)  : 查询，返回一行数据
2. row\.scan(any) ： 把一行数据，映射到结构体上这里我们需要用到指针

## 多个查询

> 查询 多个对象

```go 
// QueryStudentBy 根据年龄查询分页
func (s *student) QueryStudentBy() (data []student, err error) {
  sqlStr := "select id, name, age from student where age >= ?"

  rows, err := sqlDb.Query(sqlStr, s.Age)
  if err != nil {
    return
  }

  defer rows.Close()
  for rows.Next() {
    info := student{}
    err = rows.Scan(&info.Id, &info.Name, &info.Age)
    if err != nil {
      return
    }
    data = append(data, info)
  }

  return
}
```


### 知识点

1. sql.Qery(sqlStr,args) : 查询多个，返回数据集
2. rows 数据集需要close 释放
3. row\.Next() : 判断是否还有下一行数据集
4. row\.scan(any) ： 把该行数据映射到结构体上

## sql复用语法Prepare

```go 
sqlStr = "select id, name, age from student where age >= ? order by id Desc limit ?,? "
  stmt, err := sqlDb.Prepare(sqlStr)
  if err != nil {
    return
  }

  rows, err := stmt.Query(s.Age, skipNum, pageSize)
  if err != nil {
    return
  }

  defer rows.Close()
  for rows.Next() {
    info := student{}
    err = rows.Scan(&info.Id, &info.Name, &info.Age)
    if err != nil {
      return
    }
    data = append(data, info)
  }

```


## 事务

```go 
func Tx() (err error) {
  // 开始事务
  tx, err := sqlDb.Begin()
  if err != nil {
    log.Fatal(err)
  }

  _, err = tx.Exec("update student set age=20 where id=1")
  if err != nil {
    // 回滚事务
    tx.Rollback()
  }

  row := tx.QueryRow("select count(*) from1 student;")
  count := 0
  err = row.Scan(&count)
  if err != nil {
    log.Println("事务查询错误：", err)
    tx.Rollback()
  }

  // 提交事务
  tx.Commit()

  return
}

```


### 知识点

1. tx,err := sqlDb.BeginTx()  ： 开始事务
2. tx.Commit()  ： 提交事务
3. tx.Rollback()  :   回滚事务
