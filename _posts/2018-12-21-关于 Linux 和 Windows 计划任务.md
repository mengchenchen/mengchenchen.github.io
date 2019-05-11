---
layout: post
title: 关于 Linux 和 Windows 计划任务
subtitle: 让机器帮你做事，可以研究研究
catalog: true
tag: Linux
---

> 先说点废话，目前这个博客访问超级慢，慢到令人发指，必须必须优化优化整理整理了。
>
> 从来没有写过关于 SQL 的文章，主要是我的 SQL 有些弱，但是 SQL 又是如此的重要，要加强了。

### Windows 的计划任务

1. `Windows + R`
2. 输入 `taskschd.msc`
3. 依次点开 `任务计划程序（本地）> 任务计划库` 
4. 右侧窗口进行详细傻瓜操作

> 在 windows 下面定时执行一段程序，首先我们就需要一段程序，那程序从何而来。① 第三方获取的各种可执行程序 ② 个人编写的可执行程序
>
> 一般来说可执行程序的后缀名为 `.exe`、`.msi`、`.vbs`、`.bat` 等等，具体可百度。
>
> 如何编写 windows 程序呢？c 语言、c#、c++、java、Vbscript 等各种编程语言都可以。

#### Vbscript

微软公司的脚本对标 `Javscript` 可运行在浏览器和 `Windows` 系统桌面上，比较简单所以不能称之为语言。

手册：

* [verhuo 教程](http://www.veryhuo.com/a/manual/vbscript/)
* [W3school VBScript 教程](http://www.w3school.com.cn/vbscript/index.asp)

#### 案例 

##### 自动关机（休眠）

新建文件 `shutdown.vbs`，用记事本打开，粘贴以下代码：

```vbscript
Set WshShell = CreateObject("Wscript.Shell")
w = WshShell.Popup("下班了，需要关机吗？不操作10分钟后自动关机！", 600, "下班提醒",vbOKCancel)
If w = vbOk Or w <> vbCancel Then 
	wscript.createobject("wscript.shell").run "shutdown -h",0
End If
```

---



2018-12-28 更新如下

```vbscript
' 获取当前程序所在的文件位置
Dim strWorkDir
strWorkDir = Left(WScript.ScriptFullName,instrrev(WScript.ScriptFullName,"\")-1)

' 加载配置文件
dim fso
config = strWorkDir & "\kill.txtc"

' 设置杀掉进程
dim items
set fso = CreateObject("Scripting.FileSystemObject")
if fso.FileExists(config) then
    set f = fso.OpenTextFile(config, 1, false)
	items = f.ReadLine()
	f.Close()
	set f = nothing
	set fso = nothing
else
	If MsgBox("在休眠时需要指定关闭进程么？",vbOKCancel) = VbOk Then
		items = InputBox("输入你休眠时需要杀掉的进程，多个进程使用空格分开")
		set f = fso.CreateTextFile(config, true)
		f.Write(items)
		f.Close()
		set f = nothing
		set fso = nothing
	End If
End If

' 关机操作
Set WshShell = CreateObject("Wscript.Shell")
w = WshShell.Popup("下班了，需要休眠吗？不操作10分钟后自动关机", 600, "下班提醒",vbOKCancel)
If w = vbOk Or w <> vbCancel Then
    If Not IsEmpty(items) then
        ' 千万不要在前面加 dim，dim 只能用来声明不能赋值
        ' dim process = split(items," ")
        process = split(items," ")
        for each item in process
            WshShell.run "taskkill /f /im " & item, 0
        next
    End If
	WshShell.run "shutdown -h",0
End If
```
本次更新学到了一些关于 Vbs 的一些内容

* dim 是用来声明变量，不能直接赋值
* split 类似于 php 的 explode 把字符串分割为数组
* 字符串的拼接符号为 & 强制拼接
* 所有 cmd 命令都由它 CreateObject("Wscript.Shell") 来完成
* 单引号是注释，字符串不能使用单引号
* 取反的方法是 Not ，使用 ！ 和 <> 和 != 都是错误的

除此之外，翻阅的第三方网页在这，非常感谢！

- [popub 的使用方法](https://zhidao.baidu.com/question/585474893.html?qbl=relate_question_0&word=WshShell.Popup)

* [Vbs 模拟 include 函数](https://blog.csdn.net/wxqee/article/details/9992447)
* [vbs 的运算符](http://www.veryhuo.com/a/manual/vbscript/html/vtorivbscriptoperators.htm)
* [vbs 的 IsNull 和 IsEmpty 的区别](https://blog.csdn.net/icanlove/article/details/38086775)
* [vbscript Split函数用法详解(字符串转数组函数)](https://www.jb51.net/article/49600.htm)
* [cmd 一行运行多条命令](https://www.zybuluo.com/gongzhen/note/476036)
* [关于文件的操作](https://www.cnblogs.com/wakey/p/5798185.html)  这个作者可以关注下里面 vbs 相关的内容比较多

---

另存为文的时候设置 ANSI 否则无法执行。

这里需要提一下，保存文件记得修改编码，否则中文乱码。（编写 vbs 强烈建议使用 notepad++）

添加一条计划任务，设置每周工作日下午 5:30 执行 `shutdown.vbs` 程序，如果加班的情况选择否即可。

配合`WakeupOnStandBy`早上 8:30 自动唤醒，美美哒。

### Linux 的计划任务

**以下内容均为转载，[传送门](https://blog.csdn.net/gaozhigang/article/details/79462177) ，侵权删，本人进行重新排版**

> crond 是linux用来定期执行程序的命令。当安装完成操作系统之后，默认便会启动此任务调度命令。crond命令每分锺会定期检查是否有要执行的工作，如果有要执行的工作便会自动执行该工作。可以用以下的方法启动、关闭这个服务:

* /sbin/service crond start //启动服务
* /sbin/service crond stop //关闭服务
* /sbin/service crond restart //重启服务
* /sbin/service crond reload //重新载入配置

#### 1.linux 任务调度的工作主要分为以下两类：

* 系统执行的工作：系统周期性所要执行的工作，如备份系统数据、清理缓存
* 个人执行的工作：某个用户定期要做的工作，例如每隔10分钟检查邮件服务器是否有新信，这些工作可由每个用户自行设置。

#### 2.crontab 命令选项:

cron服务提供crontab命令来设定cron服务的，以下是这个命令的一些参数与说明:

* crontab -u //设定某个用户的cron服务，一般root用户在执行这个命令的时候需要此参数
* crontab -l //列出某个用户cron服务的详细内容
* crontab -r //删除没个用户的cron服务
* crontab -e //编辑某个用户的cron服务

比如说 root 查看自己的 cron 设置 : crontab -u root -l

再例如，root 想删除 fred 的 cron 设置:crontab -u fred -r

在编辑 cron 服务时，编辑的内容有一些格式和约定，输入: crontab -u root -e

进入 vi 编辑模式，编辑的内容一定要符合下面的格式 : */1 * * * * ls >> /tmp/ls.txt



#### 3.cron 文件语法

|分|小时|日|月| 星期|命令|
| ---- | ---- | ---- |
|0-59|0-23|1-31|1-12| 0-6|command     (取值范围,0表示周日一般一行对应一个任务)|

#### 4.记住几个特殊符号的含义

* "*" 代表取值范围内的数字,
* "/" 代表"每",
* "-" 代表从某个数字到某个数字,
* "," 分开几个离散的数字

#### 5.举几个例子

```shell
# 指定每小时的第5分钟执行一次ls命令
> 5 * * * * ls
# 指定每天的 5:30 执行ls命令
> 30 5 * * * ls
# 指定每月8号的7：30分执行ls命令
> 30 7 8 * * ls
# 指定每年的6月8日5：30执行ls命令
> 30 5 8 6 * ls
# 指定每星期日的6:30执行ls命令[注：0表示星期天，1表示星期1，以此类推，也可以用英文来表示，sun表示星期天，mon表示星期一等。]
> 30 6 * * 0 ls
# 每月10号及20号的3：30执行ls命令[注：”,”用来连接多个不连续的时段]
> 30 3 10,20 * * ls
# 每天8-11点的第25分钟执行ls命令[注：”-”用来连接连续的时段]
> 25 8-11 * * * ls
# 每15分钟执行一次ls命令(每个小时的第0 15 30 45 60分钟执行ls命令)
> */15 * * * * ls
# 每个月中，每隔10天6:30执行一次ls命令(即每月的1、11、21、31日是的6：30执行一次ls命令)
> 30 6 */10 * * ls
# 每天7：50以root 身份执行/etc/cron.daily目录中的所有可执行文件(注：run-parts参数表示，执行后面目录中的所有可执行文件)
> 50 7 * * * root run-parts /etc/cron.daily
```

#### 6.新增调度任务可用两种方法：

1. 在命令行输入: crontab -e 然后添加相应的任务，wq存盘退出。
2. 直接编辑/etc/crontab 文件，即vi /etc/crontab，添加相应的任务
