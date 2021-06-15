---
layout: post
title: WSL-Ubuntu 下安装 mcrypt 扩展
author:     mengchenchen
subtitle: 在 Linux 下安装 php 扩展很多时候需要依赖外部软件，挺麻烦的……
catalog: true
tags:
  - Swoole
  - PHP扩展
  - Linux
  - WSL
---

## 通过 PECL 安装

```shell
sudo pecl install mcrypt
```

安装的目录 `/tmp/pear/dowload`，查看是否下载成功

### 报错一：更新 pecl.php.net

如果报错

```
WARNING: channel "pecl.php.net" has updated its protocols, use "pecl channel-update pecl.php.net" to update
```

解决办法

```shell
pecl channel-update pecl.php.net
```
### 报错二：channel-add: temp_dir is not writabl

然后又出现了

```
channel-add: temp_dir is not writable: "/tmp/pear/install" - You can change this location with "pear config-set temp_dir"
```

这句的意思是 `/tmp/pear/install`没有权限

修改权限

```shell
sudo chmod -R 777 /tmp/pear/install/
```

### 报错三：先安装 libmcrypt

```shell
configure: error: mcrypt.h not found. Please reinstall libmcrypt.
ERROR: `/tmp/pear/temp/mcrypt/configure --with-php-config=/usr/bin/php-
config --with-mcrypt' failed
```

解决方法：

```shell
wget https://nchc.dl.sourceforge.net/project/mcrypt/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz libmcrypt
cd libmcrypt
./configure
make
make install
```

## 配置 ini

如果使用的是 apache2

```shell
# 如果未初始 root 密码，使用 sudo passwd root 设置密码，设置成功后，进入 root
su
# 写入配置文件
echo 'extension=mcrypt.so' >> /etc/php/7.4/mods-available/mcrypt.ini
cd /etc/php/7.4/cli/conf.d/ && ln -s ../../mods-available/mcrypt.ini 20-mcrypt.ini

# 重启 apche2 才能生效
/etc/init.d/apache2 restart
```

如果使用的是 httpd 传统的配置到 php.ini 文件就行了，这里就不描述了。

## 参考文章

* [https://blog.csdn.net/hw_henry2008/article/details/6703115](https://blog.csdn.net/hw_henry2008/article/details/6703115)

* [https://blog.csdn.net/resilient/article/details/93461279](https://blog.csdn.net/resilient/article/details/93461279)

**注意：这里面看到说是要依赖 mhash 这个软件，但是我好像没有安装也是没有问题的。**

