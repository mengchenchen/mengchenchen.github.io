---
title: 通过GithubPage搭建一个静态博客 （一）
tag: githubpage
---
>没空间、没域名..... 想做一个网站如何实现？恐怕使用 GitHub Page + jekyll 是最好的选择了，GitHub给你提供域名及空间，jekyll给你提供引擎支持及样式模板，你需要做的只是写文章就行了，如果你有兴趣也可以开发jekyll模板。当然这样的结合目前只能是实现静态的网站，如果你想实现复杂的功能及数据存储，恐怕还是需要购买专业的服务器做动态网站。

#### 准备工作

* 一个添加过ssh key 的 github账号
* 可以使用git命令的工具，如 <a href='https://git-scm.com/downloads'>git base</a>

<span style='color:#912222'>请务必确保满足以上条件。</span>

##### 一、 新建GitHubPage仓库

1.1 登陆你的<a href='https://github.com/'>GitHub</a> 

1.2 创建仓库

点击右上角加号标志选择 <a href='https://github.com/new'>New repository</a> ,

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%871.jpg'>

这里我输入的是mengchenchen.github.io ，你需要将mengchenchen替换成你的用户名

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%872.png' width="100%">

<a href='https://github.com/'>返回GitHub首页</a> ，如果看到你刚才创建的仓库，此步完成。

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%873.png'>

##### 二、本地文件关联仓库

① 选择项目需要存放的文件目录：如 D:\www

② 右键文件夹空白处右键，选择git base here

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%876.png' style='height:200px;'>

> 输入命令克隆github仓库 : **git clone 你新建的仓库地址**

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%877.png'>

命令完成后 D:\www 文件夹下会创建一个mengchenchen.github.io 这里只是演示，以你的项目名称为准。

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%878.png'>

接下来需要进入到 mengchenchen.github.io 文件夹下，以后的工作都在这个文件下开展。

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%879.png'>

> 此前文件夹下只有一个.git 文件，因为我们的项目本身是空的。 

##### 三 、测试

① 新建一个文件

首先我们创建一个index.html 文件，

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%8710.png'>

可以输入一句这样的一句话，当然你可以随便写这是随意的。只要你记得就好。

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%8711.png'>



② 推送文件到github仓库

> 注意：这里只作为演示使用，具体命令请参考 git文档

依次执行以下命令

> git add .			
>
> git commit -m test
>
> git push

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%8712.png' style='width:100%'>

③ 回到你的github主页，查看 mengchenchen.github.io 仓库多了一个index.html文件

④ 最后测试结果

使用浏览器在地址栏输入（输入填你自己的）。以我的举例：mengchenchen.github.io 

<img src='http://ox2pfy76y.bkt.clouddn.com/%E5%9B%BE%E7%89%8713.png'>

浏览器会打开刚才创建的index.html，可以看到我们刚才输入的那句话。



> 以上的这些图片全部存在七牛云存储上

> **谁让typora不支持相对路径，而且截图不能直接粘贴**
>
> 我先粘贴图片到office文档上 > 右键一个个图片另存为到本地  > 登陆七牛后台上传云存储 > 在文章中一个图片一个图片对照着添加生成的外链

**jekyll部分很遗憾和这篇文章没能写在一块，后续会补上**



<br><span style='padding:15px;display:block;background:#333;color:#f5f5f5;font-size:14px'>这篇文章主要作为自己学习记录、笔记。学习过程中避免不了的错误会出现在文章中，欢迎各位读者指出错误。</span>