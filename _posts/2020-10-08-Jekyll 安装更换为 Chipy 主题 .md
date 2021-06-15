---
layout: post
title: Jekyll 安装更换 Chipy 博客主题
catalog: true
tags: 
 - Jekyll
 - Ruby
 - Linux
 - Gitee Page
---

## 环境要求

### [Ruby](http://www.ruby-lang.org/zh_cn/)

 *Ruby*是一种纯粹的面向对象编程语言，它由日本的松本行弘(まつもとゆきひろ/Yukihiro Matsumoto)创建于1993年。

```shell
# 安装ruby
sudo apt-get install ruby
# 查看 ruby 版本
ruby -v
# 查看帮助
ruby -h
```

### [RubyGems](https://rubygems.org/)

 *RubyGems* 是 Ruby 的一个包管理器,它提供一个分发 Ruby 程序和库的标准格式,还提供一个管理程序包安装的工具。

```shell
# 安装
gem install mygem
# 卸载
gem uninstall mygem
# 列出已安装的gem：
gem list --local
# 列出可用的gem
gem list --remote
```

#### 切换国内镜像

https://gems.ruby-china.com/

## 安装主题 chirpy

```shell
git clone https://github.com/cotes2020/jekyll-theme-chirpy.git blog
cd blog
bundle install
```

### nokogiri 报错

[nokogiri 官网](https://nokogiri.org/tutorials/installing_nokogiri.html)

```shell
# 安装依赖的软件
sudo apt-get install build-essential patch ruby-dev zlib1g-dev liblzma-dev
# 单独安装 nokogiri
gem install nokogiri
# 重新更新一下
bundle update
```

### 启动 jeykll

```shell
bundle exec jekyll serve
```

看到 **Server address: http://127.0.0.1:4000/**，直接打开网址即可。