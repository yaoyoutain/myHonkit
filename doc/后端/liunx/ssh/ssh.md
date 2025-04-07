# ssh

## 目录

- [配置账户免密登录](#配置账户免密登录)
  - [windos cmd  生成key](#windos-cmd--生成key)
  - [windos  .ssh config 多ssh 管理](#windos--ssh-config-多ssh-管理)
- [相关命令 ](#相关命令-)
  - [ssh-keygen  ](#ssh-keygen--)

# 配置账户免密登录

## windos cmd  生成key

```bash 

# 生成rsa key 备注-c： 树莓派 , 生成到指定目录 -f
ssh-keygen -C '树莓派' -f smp_id_rsa

#然后回车生成key
# 看输出信息看生成的文件放在 哪里 
# 一般在账号/.ssh文件下 
id_rsa 是私钥
id_rsa.pub 是公钥，公钥需要放到服务器上


```


## windos  .ssh config 多ssh 管理

win目录：用户/.ssh/config

```bash 
Host 目标主机标识
  HostName 目标主机实际ip
  Port 端口
  User 用户
  # 强制使用publickey模式
  PreferredAuthentications publickey   
  # 使用秘钥地址
  IdentityFile C:\Users\xxx\.ssh\my-gitea

```


# 相关命令&#x20;

```bash 

## 创建
ssh-keygen -C '树莓派' -f smp_id_rsa 
-t 秘钥类型rsa
-C 提供一个注释
-f 指定秘钥生成的文件名称

# 测试
ssh -T （config Host文件）git@github.com

# 将公钥复制到远程主机上
ssh-copy-id -i (路径) ldz@192.168.0.1


```


## ssh-keygen &#x20;

-t 秘钥类型rsa

-C 提供一个注释

-f 指定秘钥生成的文件名称
