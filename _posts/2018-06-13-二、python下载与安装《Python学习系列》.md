---
title: 《Python学习系列》2、python的下载与安装
tag: python
---

#### 下载

版本：3.5

系统：windows（其他系统不管）

官网：https://www.python.org/

国内镜像：https://pan.baidu.com/s/1kU5OCOB#list/path=%2Fpub%2Fpython

#### 安装

1、选择电脑安装电脑账户

2、选择安装目录（以实际安装为准，网上盗来的图）

windows版本的安装是傻瓜式的，在选择安装目录后一路点击Next >（记住你的安装目录即可）

#### 设置环境变量
一、**命令行**直接输入 

```
path=%path%;C:\Python27
```

把`C:\Python27` 替换成你的python安装安装目录

二、**计算机属性**

按下window键+pause markdown插入图片break键->高级系统设置->高级->环境变量->系统变量->Path->编辑，将Python安装目录新增至path（win10列表直接添加，win7以；为分割添加）

![avatar](http://www.runoob.com/wp-content/uploads/2013/11/201209201707594792.png)

#### Python运行模式
一、**交互式**：设置过Python环境变量在任何目录下进入命令行模式，输入Ptython
``` 
C:\Users\Administrator>python
Python 2.7.12 (v2.7.12:d33e0cf91556, Jun 27 2016, 15:24:40) [MSC v.1500 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
在>>>后面输入要执行的python语句就实现了交互式（但是在学C#的时候称为控制台模式）

二、**命令行脚本模式**

```
C:\Users\Administrator>python a.py
```

通过python命令直接执行已经存在的py文件，注意这里需要到py所在路径执行

#### 延伸
1、Pycharm：IDEA 集成开发环境，和phpstorm同根生，功能也差不多
2、Pycharm 激活方式
```
	通过修改host文件和注册码激活，推荐lanyu；
	通过监听地址激活，推荐成都没有派对；
	pychram破解版，绿色版；
	其他激活软件；
```
3、借用菜鸟教程的两个笔记：
```
对于 Python 学习的新手来说，安装 Anaconda 包管理软件是一个不错的选择，可以减少很多后续安装 Python 各种包的麻烦。在 Anaconda 自带的 notebook 进行代码的编写要比 IDE 和 Terminal 的体验好得多。

Anaconda 的下载地址：https://www.anaconda.com/download/
Windows 如果使用终端进行 Python 编程时，建议对终端进行一定的美化。

Cmd 美化参考：https://zhuanlan.zhihu.com/p/31904974

```
```
如果需要使用 Pycharm 又恰好是学生的话，可以免费申请享用高大上的Professional版本。

申请地址：https://www.jetbrains.com/student/
在填写学校邮箱申请完成后，会收到一封激活邮件。点击链接激活后会收到一封包含下载地址链接的邮件，就可以享用 Jetbrains 的所有专业软件了。
```
4、<b>注意</b> :如果在安装python前打开任何cmd窗口都需要关闭再重新打开

<span style="padding:10px;display:block;color:white;background:black;font-size:12px">
文章中用到的部分图片和部分内容来自以下三个网页<ul><li>https://www.cnblogs.com/hongten/p/hongten_python_install.html</li><li>https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001374738150500472fd5785c194ebea336061163a8a974000</li><li>http://www.runoob.com/python/python-install.html</li></ul></span>





