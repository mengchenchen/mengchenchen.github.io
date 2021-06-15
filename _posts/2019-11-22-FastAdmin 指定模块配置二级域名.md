---
layout: post
title: FastAdmin 绑定二级域名
catalog: true
tags: 
 - ThinkPHP
 - FastAdmin
 - PHP
---

## FastAdmin 绑定二级域名

### 说明
注：以下的域名以 [test.com](http://test.com/) 为例

平时访问 fastadmin 的 url 是这样的

```
test.com/admin/dashboard?ref=addtabs
```

想在我们想要把中间的 admin 给去掉，使用二级域名 [backend.test.com](http://backend.test.com/) ，最后会变成这样

```
backend.test.com/dashboard?ref=addtabs
```


### 第一步、 先在 host 文件中添加
```
127.0.0.1    test.com    backend.test.com
```

### 第二步、 到 web 服务器添加相应的虚拟域名

```
server {
        ###SiteName  project1
        listen       *:80;
                ### 就是这样一段话
        server_name  test.com     backend.test.com
        root         "D:/www/fastadmin/public";
        #error_log    "D:/Visual-NMP-x64/logs/Nginx/project1-error.log";
        #access_log   "D:/Visual-NMP-x64/logs/Nginx/project1-access.log";
        #autoindex    on;
        #index        index.php index.html index.htm;
        # 这句话的作用是用 pathinfo 的模式，一般来说都需要添加这句话
        location / {
            if (!-e $request_filename) {
                rewrite  ^(.*)$  /index.php?s=/$1  last;
            }
            index  index.html index.htm index.php l.php;
            autoindex  off;
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


### 第三步、修改 fastadmin 的配置文件

config.php

```
// 设置默认访问模块
'default_module' => 'index',
// 域名部署是否开启
'url_domain_deploy' => 'true'
```

  route.php   

```
// backend 代表的是二级域名名称，admin 代表的是项目中的模块
'__domain__' => [
    'backend' => 'admin',
    'api' => 'api',
],
```


### 测试

分别打开 [test.com](http://test.com/) 和 [backend.test.com](http://backend.test.com/) 如果分别访问的是 index 模块和 admin 模块，就表示我们的配置二级域名指定模块已经成功了