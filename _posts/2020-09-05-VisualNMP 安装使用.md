---
layout: post
title: Visual-NMP 使用指南
subtitle: windows 下好用的 php 集成环境
catalog: true
tag: 工具
---

## 下载地址





## 自由切换 php 版本

###  一、下载并配置 php 版本

之前一直以为 visulNMP 不能切换 php 版本，后来发现在主界面可以一键切换，但是速度特别的慢，之前已知都
没有下载成功过。

今天我又尝试着去升级 php 版本，使用主界面的下载 php 版本，发现还是下载不了，最后尝试着到 php 官网下载 ZIP 版本，其他的一般都是 linux 下的
https://windows.php.net/download#php-7.3

下载并解压文件放入 /visualNMP/bin/php/ 目录之下，注意新的 php7 版本是没有 php.ini 文件的，
https://blog.csdn.net/wang740209668/article/details/73278221

完成 php.ini 重命名后，进行相关的配置

**使用 php -m 查看是否有模块不存在，extension_dir 的配置是否正确，默认是 C 盘根目录，记得改下！**

 **1、打开需要的扩展（默认所有的扩展都是关闭的）** 
```
extension=openssl
extension=fileinfo
extension=curl
extension=gd2
extension=mysqli
extension=pdo_mysql
```

修改完成后保存

 **2、配置环境变量，安装 composer** 

> 这一步千万不能忘记

 **3、进入命令行** 
```
# 刷新env
refreshenv
# 检查 php 是否正常
php -v
# 如果这里出现了 PHP Warning:  PHP Startup: Unable to load dynamic library 'curl' (tried: C:\php\ext\curl (找不到指定的模块。),
# C:\php\ext\php_curl.dll (找不到指定的模块。)) in Unknown on line 0，这个说明扩展的路径配置问题，我们进入
php.ini 文件，搜索并编辑为 extension_dir = '最好使用绝对路径的 ext 文件目录'，如果此步配置正确，查看有无
相应的扩展文件，如果没有请下载或者关闭相应的扩展加载。

```

### 二、配置 nginx

打开 visualNMP/bin/nginx/Nginx_Serv.ini，找到并编辑 
```
php-cgi.exe_path=[php版本目录]\php-cgi.exe。
```

### 三、重启 nginx


 **php 配套** 

- [手动安装 composer](https://getcomposer.org/doc/00-intro.md#installation-windows)
- [手动安装 phpunit](http://www.phpunit.cn/documentation.html)

### 四、注意事项：

1. 查看环境变量是否配置成功，这里会存在缓存的问题。
2. 手动安装完成 php 之后使用 php -m 查看是否有模块不存在，因为默认的 php.ini 文件的扩展目录是 c 盘的，如果你的 php 目录不是这里的话，就会报错，还需要把 extenstion_dir 目录修改下。

## 虚拟站点 404

这个来说是 Nginx 的问题，这里也写一下，一般配置 TP 或者是 Laravel 的 Public 目录之后，发现访问不了。这个时候要在 Nginx 的 nginx.conf 目录下修改一下。

```nginx
server {
        ###SiteName  ylxp
        listen       *:80;
        server_name  ylxp_test.com;
        root         "E:/project1/public";
        error_log    "E:/software/Visual-NMP-x64/logs/Nginx/ylxp-error.log";
        #access_log   "E:/software/Visual-NMP-x64/logs/Nginx/ylxp-access.log";
        
        # 这里注释掉
        #autoindex    on;
        #index        index.php index.html index.htm;
    
    	# 加上这一句话，是 tp 类项目的伪静态写法。
        location / {
            index  index.html index.htm index.php;
        
            #主要是这一段一定要确保存在
            if (!-e $request_filename) {
                rewrite  ^(.*)$  /index.php?s=/$1  last;
                break;
            }
        }

        location  ~ [^/]\.php(/|$) {
                fastcgi_split_path_info  ^(.+?\.php)(/.*)$;
                if (!-f $document_root$fastcgi_script_name) {
                        return 404;
                }
                fastcgi_pass   127.0.0.1:9001;
                fastcgi_index  index.php;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                fastcgi_param  PATH_INFO        $fastcgi_path_info;
                fastcgi_param  PATH_TRANSLATED  $document_root$fastcgi_path_info;
                include        fastcgi_params;
        }
    }
```

