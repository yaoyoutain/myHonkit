# ssh 链接

## 目录

- [生成key ](#生成key-)
- [一台 电脑多个ssh](#一台-电脑多个ssh)

## 生成key&#x20;

```git 
ssh-keygen -t 目标目录文件名称 -C "注释"
```


中间有三次回车

```git 
// 打开目录
ls ~/.ssh/

// 打开公钥
cat ~/.ssh/id_ed25519.pub

// 测试
ssh -T 用户名@名称

```


# 一台 电脑多个ssh

```git 
touch ~/.ssh/config

Host 名称
    HostName 地址
    User 用户名
    IdentityFile ~/.ssh/id_rsa_github 私钥地址



```
