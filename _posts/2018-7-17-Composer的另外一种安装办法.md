---
title: Composer 的另外一种安装办法
tag: 日常
---

> 话说安装composer步骤挺简单的，但是往往在安装的最后一到两步出现网络加载等错误。之前在网上也相应找了其他的方法，最终找到了稳定的方法就记录在wps的云文档上，但是每到一个新地方都需要安装打开wps找到composer的安装办法，实在是有些麻烦，今天把它写到博客上。

#### 第一步：下载composer.phar

下载地址：https://getcomposer.org/download/ 

进入页面Ctrl+F 搜索 ` Manual Download`，选择需要下载的版本

将下载好的composer.phar文件移动到当前php的安装目录中

#### 第二步：新建composer.bat

新建一个composer.bat文件，内容如下

```
@ECHO OFF
php "%~dp0composer.phar" %*
```

双击此文件运行

#### 第四步：测试

打开cmd窗口，输入composer -v



#### 注意事项

* php需要配置环境变量

* 执行composer.bat文件之前，确保cmd窗口处于关闭状态

  