---
title: 通过githubpage搭建一个静态博客
tag: githubpage
---
### 准备工作

* 一个添加过ssh key 的 github账号
* 可以运行的ruby环境
* 可以使用git命令的工具，如 <a href='https://git-scm.com/downloads'>git base</a>

<span style='color:#912222'>请务必确保满足以上条件。</a>

##### 一、 新建GitHubPage仓库

1.1 登陆你的<a href='https://github.com/'>GitHub</a> 

1.2 创建仓库

点击右上角加号标志选择 <a href='https://github.com/new'>New repository</a> ,



<a href='https://github.com/'>返回GitHub首页</a> ，如果看到你刚才创建的仓库，此步完成。

1.3 本地文件关联仓库

① 选择项目需要存放的文件目录：如 D:\root 

② 右键文件夹空白处右键，使用git base，输入命令克隆github仓库

> git clone 你新建的仓库地址

命令完成后 D:\www 文件夹下会创建一个mengchenchen.github.io 这里只是演示，以你的项目名称为准。

1.4 测试

① 首先我们创建一个index.html 文件，通过记事本随便打上一句话保存。

② 推送文件到github仓库

> 注意：这里只作为演示使用，具体命令请参考 git文档

依次执行以下命令

> git add .			
>
> git commit -m test
>
> git push

③ 回到你的github主页，查看 mengchenchen.github.io 仓库多了一个index.html文件

④ 最后测试结果

使用浏览器在地址栏输入（输入填你自己的）。以我的举例：mengchenchen.github.io 

