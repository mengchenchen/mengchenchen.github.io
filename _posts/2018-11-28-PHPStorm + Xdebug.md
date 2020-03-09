---
layout:     post
title:      PHPStorm + Xdebug
subtitle:   Debug 新姿势
date:       2018-12-12
author:     mengchenchen
catalog: true
tags:
    - PHP
---

## 第一步：下载 php_xdebug.dll 扩展和 xdebug helper 插件

### ① php_xdebug.dll

#### 下载并安装

* [官网](https://xdebug.org/download.php)

![post-phpstormxdebug-phpinfo](/img/in-post/post-phpstormxdebug-phpinfo.png)

> **注意：把下载下来的 xdebug.dll 移动到 php 安装目录的 ext 目录。**

### ② Xdebug helper

#### 下载并安装

* [google 商店](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=zh-CN)
* [国内第三方](https://www.crx4chrome.com/crx/1716/)

## 第二步：修改 php.ini 配置

#### 配置 php.ini

在 php.ini 追加

```ini
[XDebug]
; 这个就是刚才下载的 xdebug.dll 
zend_extension=php_xdebug-2.5.1-5.6-vc11-nts.dll
xdebug.profiler_append = 0
xdebug.profiler_enable = 1
xdebug.profiler_enable_trigger = 0
xdebug.profiler_output_dir ="D:\phpStudy\tmp\xdebug"
xdebug.trace_output_dir ="D:\phpStudy\tmp\xdebug"
xdebug.profiler_output_name = "cache.out.%t-%s"
xdebug.remote_enable = 1
xdebug.remote_handler = "dbgp"
xdebug.remote_host = "127.0.0.1"
xdebug.remote_port = 9000
xdebug.remote_mode = "req"
; 这个和后面是进行关联的
xdebug.idekey = PHPSTORM
```

以上具体的参数可以去官网进行搜索

## 第三步：配置 PHPSTORM 和 xdebug helper

### 配置 PHPStorm

` Ctrl + Alt + s ` 打开设置

![1](/img/in-post/post-phpstormxdebug-phpstormconfig1.png)

![2](/img/in-post/post-phpstormxdebug-phpstormconfig2.png)

![3](/img/in-post/post-phpstormxdebug-phpstormconfig3.png)

### 配置 xdebug helper

右键扩展->选项

![1](\img\in-post\_2020030910390439SS.png)

## 最后一步：使用

域名 `xdebugtest.com`

① 打开 xdebug helper 调试开关

![1](\img\in-post\_2020030910231023SS.png)

② 打开 phpstrom 监听 xdebug 开关

![1](\img\in-post\_2020030910411141SS.png)

③ 打断点开始调试

打断点

![1](\img\in-post\_2020030910571257SS.png)

打开 `xdebugtest.com` 并刷新页面，如下

![2](\img\in-post\_2020030910441344SS.png)

快捷键 F7 继续向下逐步执行进行调试。



