---
title: 为Github Page增加评论功能
subtitle: 给个评论，感谢诸位
tag: githubpage
---

## 前言

> 博客第一篇文章中写到，本博客采用 jekyll + github page技术实现。不涉及任何的后台操作，在此之前我们如果想要实现评论的功能要考虑使用`多说`,`diqus`,`网易评论`等等评论的平台插件，如今他们统统关闭。今天我们就来探讨静态github page网站添加评论功能的解决方案。
>
> 很早之前，我们的评论的数据都存储在Mysql表中，如今前端技术的逐步强大，对于简单的后端数据依赖越来越小。`GitHub`作为全球最大的开发者聚集地，提供`GitHub Page`让我们可以在没有服务器的情况下建站，得益于开源，我们可以直接通过`GitHub`获取各种优秀的插件以及主题、应用等。例如`Hexo`,`Ghosts`，以及本站使用的`jekyll`等等博客静态建站方案。

## 解决

- [Gitment](https://github.com/imsun/gitment) 作者：[孙土权](https://imsun.net/)
- [Gitalk](https://gitalk.github.io/)

就目前而言，我为本站添加评论功能时，主要接触到两个开源项目。两者的解决方案都是

- 使用`Github Issues`作为评论的存储空间
- 使用`Github`账号登陆评论
- 使用之前需要进行初始化

因为是刚加入`Gitalk`的评论功能，关于一些细节参数等没有认真的看文档。不过在部署的过程中也发现了一些基本问题这里不展开讨论，在之后忙里偷闲之后可以看看这个 

> // TODO  [如何自动初始化 Gitalk/Gitment 评论](https://www.colabug.com/1784203.html)

### 开始

前面也说过，所有评论的功能都是基于`Issue`实现，所以我们功能实现需要得到`GitHub`的授权支持。

接下来是使用`Gitalk`来进行演示，`Gitment`的使用方法大同小异。

####  1、OAuth Application [注册认证应用]

点击这里[传送门](https://github.com/settings/applications/new)，Register a new OAuth application

**这里简单的介绍下：**

* Homepage URL [你需要进行授权的应用主页地址，如`https:mengchenchen.github.io]`
* Authorization callback URL  [授权成功后回调地址，继续使用`https:mengchenchen.github.io`]

成功之后我们得到client_id和secret_id

#### 2、 [_config.yml] 修改配置文件

请记住我们使用的是`jekyll`，所以在项目的根目录下会有一个`_config.yml`文件，打开它添加以下代码。

```yaml
gitalk:
  enable: true    #是否开启评论
  clientID: ***                            #生成的clientID
  clientSecret: *****    #生成的clientSecret
  repo: mengchenchen.github.io    #仓库名称
  owner: mengchenchen    #github用户名
  admin: mengchenchen	
  distractionFreeMode: true #是否启用阴影遮罩
```

#### 3、HTML添加至 [_layout/post.html]

记得找到合适的位置，把以下代码复制粘贴过去。

```html
<!--Gitalk评论start  -->
{% if site.gitalk.enable %}
<!-- 引入Gitalk评论插件  -->
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>
<div id="gitalk-container"></div>
<!-- 引入一个生产md5的js，用于对id值进行处理，防止其过长 -->
<!-- Thank DF:https://github.com/NSDingFan/NSDingFan.github.io/issues/3#issuecomment-407496538 -->
<script src="{{ site.baseurl }}/js/md5.min.js"></script>
<script type="text/javascript">
    var gitalk = new Gitalk({
        clientID: '{{site.gitalk.clientID}}',
        clientSecret: '{{site.gitalk.clientSecret}}',
        repo: '{{site.gitalk.repo}}',
        owner: '{{site.gitalk.owner}}',
        admin: ['{{site.gitalk.admin}}'],
        distractionFreeMode: {{site.gitalk.distractionFreeMode}},
    id: md5(location.pathname),
    });
    gitalk.render('gitalk-container');
</script>
{% endif %}
<!-- Gitalk end -->
```

**注意**：这里面我们引入了`md5.min.js`文件，如果你没有这个文件可以到我们博客开源项目下找到这个文件。

太详细就不讲了，可以看官方文档，接下来你要做的事情是这样的：

>1. 推送代码到`GitHub`
>2. 测试`Gitalk`
>3. 修复 bug
>4. 初始化认证
>5. 愉快的使用评论功能

#### 引用与参考

* [BY Blog](http://qiubaiying.top/) 查看文章时看到评论框，才引发了这篇文章。主要参考源代码。
* [百度](http://baidu.com) 所有搜索查找数据来自百度

> 本文章为作者原创文章，尊重作者劳动成功，转载或引用文章请注明出处：https://mengchenchen.github.io/。文章内容不能作为权威标准，如有不当望各位读者指出批评。作为一名年轻开发的学习人员，与君共勉。

