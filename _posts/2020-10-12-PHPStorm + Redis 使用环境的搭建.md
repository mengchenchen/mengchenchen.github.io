---
layout: post
title: WSL + PHPStorm + Redis 使用环境搭建
catalog: true
tags: 
 - 工具
 - PHPStorm
 - Redis
---

## WSL - Ubuntu

上面配置完成 `PHPStorm` 之后，直接通过 `ssh` 连接到 `WSL-Ubuntu` 的 `redis-server` 服务中。

### Redis-Server

redis 服务端

```shell
# 安装
sudo apt install redis-server
# 查看端口是否被占用：
netstat –ntlp |grep 6379
# 启动服务，不使用 sudo 则没有权限退出，默认的是作业进程使用 ctrl+c 结束进程，可以通过修改配置文件为守护进程
sudo redis-server
# 如果没有 sudo，使用 kill -9 pid 杀掉进程即可
```

#### 获取文件安装位置

如果无法找到 Redis 的安装位置，提供一个思路；首先获取环境变量的目录，从那些目录里面去找到 redis 的安装位置。

#### 配置文件位置

默认的配置文件位置是 `/etc/redis/redis.conf`，如果打开之后是一片空白的话，是因为文件的权限不对

```shell
# 添加权限
sudo chmod 755 redis.conf
# 编辑文件，就可以看到内容了
sudo vim redis.conf
```

### Redis-cli

redis 客户端

```shell
# 安装
sudo apt install redis-cli
# 进入 redis 命令行
redis-cli
```



## PHPStorm 安装 Redis 插件

### 安装

打开 PHPStorm 依次点击`File > Settings > Plugins `，输入框输入 `Redis` 查找。

![Settings 163115.png](https://gitee.com/brymg/images/raw/master/blog/Settings 163115.png)

选择安装 `redis simple` 即可，其他的为收费插件且不可用。

### 配置

安装完成之后重启 `PHPStorm`，再次打开设置会看到最下方的 `NoSql Server`

![Settings 163726.png](https://gitee.com/brymg/images/raw/master/blog/Settings 163726.png)

直接点击 Services 下面的 ”+“ 号设置进行连接，上面的 `Path to Redis DB Cli` 等 ☞ 的是在 PHPStorm 环境中运行所以来的工具，如果本地没有安装可以直接忽略。



