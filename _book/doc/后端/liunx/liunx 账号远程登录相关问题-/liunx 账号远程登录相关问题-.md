# liunx 账号远程登录相关问题&#x20;

1. 开启root 远程登录权限
2. 开启普通账户免密登录
3. 开启root账号免密登录

liunx 配置文件vi /etc/ssh/sshd\_config

注意修改配置文件需要重启sshd服务 service ssh restart

配置解析

```bash 
// 开启root登录
PermitRootLogin yes

// 开启免密登录
PasswordAuthentication no
PermitEmptyPasswords yes

```


重启sshd服务 service ssh restart

```vue 
// 添加账号

adduser 账号
```
