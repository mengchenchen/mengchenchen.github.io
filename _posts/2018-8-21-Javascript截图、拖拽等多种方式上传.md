---
title: Javascript截图、拖拽等多种方式上传
tag: Javascript
---

首先来介绍基本使用情况，webuploader 插件用来多图上传和拖拽上传本地图片，不过webuploader不支持直接拖动网络图片、截图、qq等图片。产品要求必须加入qq图片拖拽上传，所以在此基础上新增input输入框用来复制截图和拖拽。接下来则开始介绍这些新增的操作步骤以及使用方法。

#### 截图（剪切板）上传图片

**注意事项**

1. 必须是实时剪切的图片粘贴
2. 使用`Ditto`等工具复制是不可用的
3. 从qq聊天窗口中复制的截图时不可用的

**写代码**

首先创建一个输入框用于粘贴图片`HTML`

```html
 	<!--这里我们的输入框-->
	<input type="text" id="testInput"/>
	<!--我们的图片添加地址-->
	<div id='qq_image_list'></div>
```

`JS`部分

```js
// 监听testInput的粘贴事件
document.getElementById('testInput').addEventListener('paste', function (e) {
    // 这里针对不同的浏览器做一些兼容性的操作，具体真的需要自己找找了，我真的是前段白痴
    // 添加到事件对象中的访问系统剪贴板的接口
    var clipboardData = e.clipboardData, i = 0, items, item, types;
    if (clipboardData) {
        // 用来获取剪切板的数据或者说是项目
        var items = clipboardData.items;
        if (!items) {
            return;
        }
        // 默认第一个项目
        item = items[0];
        // 查找剪切板中有没有文件(type == Files)的项
        types = clipboardData.types || [];
        for (var i = 0; i < types.length; i++) {
            if (types[i] === 'Files') {
                item = items[i];
                break;
            }
        }
        // 判断是否为图片数据
        if (item && item.kind === 'file' && item.type.match(/^image\//i)) {
            // 打印项目
            console.log(item);
            // 从这里开始就是生成一个base64的图片流
            var blob = item.getAsFile(),reader = new FileReader();
            // 读取文件后将其显示在网页中
            reader.onload = function (e) {
                var img = new Image();
                img.src = e.target.result;
                $('#qq_image_list').append(img);
            };
            // 读取文件
            reader.readAsDataURL(blob);
        }
    }
 });
```

#### 拖拽上传图片

**首先简单的介绍几种拖拽上传图片的途径和方式**

* **网络图片** 拖拽至指定区域
* **本地图片** 拖拽至指定区域
* **QQ图片** 拖拽至指定区域
* ...

其实`qq截图或者聊天记录中的图片`和`本地图片`其实是一回事情，因为`qq截图或者聊天记录中的图片`其实都是保存在本地`c盘`中的缓存目录中。不过他们之间的区别请往下面看：

##### 一、本地图片直接拖动上传

HTML 部分

```HTML
<div id='image_box'></div>
```

JS 部分

```js
var box=document.getElementById('image_box');
    box.ondragover=function (e){
     	e.preventDefault();
    }
    box.ondrop=function (e){
        var file = e.dataTransfer.files[0];
        var render = new FileReader();
        render.readAsDataURL(file);
        render.onload = function (e) {
            // 在这里我们可以进行一部上传服务器代码
            $('#image_box').append('<img src="' + this.result + '" alt="">');
        };
     }
}
```

##### 二、QQ图片拖动上传

**上面已经看到了本地图片直接拖动上传可以直接通过e.dataTransfer.files[0]获取，但是QQ图片则不可以这样。**这里走过的超级大坑，几乎调试我到崩溃的边缘。

如果你直接把**QQ的聊天记录图片或者当前截图**拖动到指定区域，你会发现他是这样的：

```HTML
[图片]
```

通过接近崩溃的残忍调试之后发现，原来QQ所产生的图片一般在电脑的这里

```
file:///C:/Users/Administrator/AppData/Roaming/Tencent/TIM/Temp/**
```

这样我们就知道了，原来qq的所产生的图片也是实实在在的本地文件。我们直接获取当前的图片的地址不就可以直接上传了吗？**可是问题就在于我不知道怎么来获取由qq拖过来的图片的url**。

再次经过残忍崩溃的调试之后，我终于看到了qq图片粘贴拖拽的新模样，他大概长这样：

```HTML
<HTML>
    <BODY>
        <DIV>
        <IMG src='file:///C:/Users/Administrator/AppData/Roaming/Tencent/TIM/Temp/**.png'>
        </DIV>
    </BODY>
</HTML>
```

原来复制或者拖动qq图片的时候产生的是一段`HTML`，多次的调试过程中我发现：**HTML和BODY两个便签有的时候时不存在的，但无论是什么时候，图片数据格式一定含有DIV和IMG两个包含标签，至于为什么标签的名称是大写的我就不得而知了。**

**我们得到这串HTML之后，就可以通过JS获取IMG的链接地址了，接下来请看代码：**

HTML 部分

```html
<!--准备材料：需要拖拽的文本一个，显示图片的div一个-->
<!--这里我们的输入框-->
<input type="text" id="testInput"/>
<!--我们的图片添加地址-->
<div id='qq_image_list'></div>
```

JS 部分

```js
var input = document.getElementById('testInput');
input.ondragover = function (e) {
    e.preventDefault();
};
input.ondrop = function (e) {
    e.preventDefault();
    // 这里是核心部分,从上面我们知道移动过来的是一段html，所以通过 text/html接收后转换为string
    var qq_image = e.dataTransfer.getData('text/html').toString();
    // 用来获取src 的正则表达式
    var regex = /<IMG.*?src="(.*?)" >/;
    // qq图片拖拽
    if (regex.exec(qq_image)) {
        // regex.exec(qq_image) 产生的是一个数组，[0]为IMG标签Dom，[1]为IMG的src
        var src = regex.exec(qq_image)[1];
        var items = e.dataTransfer.items;//获取到第一个上传的文件对象
        if (!items) {
            return;
        }
        item = items[0];
        // 保存在剪贴板中的数据类型
        types = e.dataTransfer.types || [];
        for (var i = 0; i < types.length; i++) {
            if (types[i] === 'Files') {
                item = items[i];
                break;
            }
        }
        // 判断是否为图片数据
        if (item && item.kind === 'file' && item.type.match(/^image\//i)) {
            // 创建base64的图片
            var blob = item.getAsFile(), reader = new FileReader();
            // 读取文件后将其显示在网页中
            reader.onload = function (e) {
                var img = new Image();
                img.src = e.target.result;
             	// 在这里我们可以进行一部上传服务器代码
                $('#qq_image_list').append(img);
            };
            // 读取文件
            reader.readAsDataURL(blob);
        }
    }
};
```

##### 三、网络图片拖拽上传

关于网络图片直接拖拽上传其实我现在并没有搞定，因为涉及到跨域问题。这里先大概的介绍一些基本写法，之后补写解决方案。

首先HTML部分和上面上传`qq`图片一样，这里我就不写了，直接看`JS`部分

```js
var input = document.getElementById('testInput');
input.ondragover = function (e) {
    e.preventDefault();
};
input.ondrop = function (e) {
    e.preventDefault();
    // 获取网络图片的url
    var url = e.dataTransfer.getData('text/plain');
    // 这里以下代码来自于 https://www.cnblogs.com/zhangdiIT/p/7895903.html
     getBase64(url).then(function(base64){
         console.log(base64);//处理成功打印在控制台
     },function(err){
         console.log(err);//打印异常信息
     });
};
// 传入图片路径，返回base64
function getBase64(img){
    function getBase64Image(img,width,height) {
        //width、height调用时传入具体像素值，控制大小 ,不传则默认图像大小
        var canvas = document.createElement("canvas");
        canvas.width = width ? width : img.width;
        canvas.height = height ? height : img.height;

        var ctx = canvas.getContext("2d");
        ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
        var dataURL = canvas.toDataURL();
        return dataURL;
    }
    var image = new Image();
    image.crossOrigin = '';
    image.src = img;
    var deferred=$.Deferred();
    if(img){
        image.onload =function (){
            deferred.resolve(getBase64Image(image));//将base64传给done上传处理
        }
        return deferred.promise();//问题要让onload完成后再return sessionStorage['imgTest']
    }
}
```





