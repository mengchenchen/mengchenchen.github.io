记录一个坑：本地新增文件composer 自动加载已删除文件，报错。

我的执行步骤：

* 本地新建一个 Test.php 文件
* 提交代码
* 运维拉取代码，执行composer up
* 本地删除 Test.php 文件
* 运维拉取代码
* 报错，include Test.php 文件不存在

我的调试步骤：

* 本地全局搜索 Test.php，没有找到对应文件以及引用代码
* 对照错误信息，分析判断出是 autoload include 文件出错
* 全局查找 Test.php 同级文件，在 vendor/composer/autoload_classmap.php、autoload_static.php中得到结果。
* 分析：本地没错，线上有错。在执行composer up之后出现错误，大概猜测不是本地代码错误
* 让运维进入autoload_classmap.php、autoload_static.php 文件搜索 Test.php 代码
* 让其注释，bug解决

困惑：不太理解laravel的自动加载，为什么执行composer up就会在 autoload_classmap.php文件中产生所有文件对应的路径信息。