---
layout:     post
title:      重新编译 Swoole 并开启 Openssl
author:     mengchenchen
subtitle: 解决 you must configure with `--enable-openssl` ……
catalog: true
tags:
  - Swoole
  - PHP扩展
  - Linux
  - WSL
---

最近使用 Hyperf 的时候，在使用 CURL 请求外部的 `https` 链接回报这样的错误：

**you must configure with `--enable-openssl` to support ssl connection when ……**

它提示我必须配置 `--enable-openssl` ，虽然我知道这句话的文字意思，但是并不知道具体怎么操作才能进行配置，因为我并不知道他的具体执行步骤或使用流程。经过昨天的相关搜索和验证，弄清了这个东西应该怎么去配。

## 安装 `openssl`

查看是否安装 `openssl`

```shell
openssl
```

未安装的时候使用命令安装：

```shell
sudo apt install openssl
```

获取 `openssl` 的安装位置

一般来说默认位置是 `/usr/bin/openssl`

## 重新编译 `Swoole`

首先要知道 php 安装扩展的时候，分为手动编译 `phpize` 和命令 `pecl` 安装。

### 1、PECL 方式

```shell
# 超级管理运行
su
# 使用 pecl 更新 swoole 扩展
pecl upgrade swoole
# 上面命令会进行编译安装 swoole 扩展，耐心等待！在等待的过程中千万不要按回车键，因为他会延迟到下一步的执行，会错过询问的操作确认！
# 知道等待询问语句在 enable openssl support? [no] : 输入
yes --with-openssl-dir=/usr/local/openssl
# 以上的 /usr/local/openssl 就是你的 openssl 安装位置，进行修改即可
```

### 2、PHPIZE 方式

 这里可以参考 [安装Swoole](https://wiki.swoole.com/#/environment)

```shell
# 超级管理运行
su
# 下载安装 swoole
git clone https://gitee.com/swoole/swoole.git
# 切换到 swoole 目录
cd swoole
# ubuntu 没有安装 phpize 可执行命令：sudo apt-get install php-dev 来安装 phpize
phpize
# 配置 openssl
./configure --enable-openssl --with-openssl-dir=/usr/bin/openssl
# 安装
make && sudo make install
```

### 解释

这里的错误属于安装编译 swoole 的步骤，设计到的知识

* Linux 的源码安装流程，`./configure` 和 `make` 的使用
* PHP 安装扩展，Windows 的 `dll` 安装，Linux 的 `PECL` 和 `phpzie` 安装；swoole 不支持 Windows 平台。

## 参考链接

* [https://wiki.swoole.com/#/environment?id=%e7%bc%96%e8%af%91%e9%80%89%e9%a1%b9](https://wiki.swoole.com/#/environment?id=%e7%bc%96%e8%af%91%e9%80%89%e9%a1%b9)

* [https://cloud.tencent.com/developer/article/1550797](https://cloud.tencent.com/developer/article/1550797)

