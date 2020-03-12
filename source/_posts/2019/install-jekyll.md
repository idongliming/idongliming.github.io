---
title: 在windows环境下安装jekyll
tags:
  - jekyll
categories: 学习笔记
date: 2019-01-30 13:26:13
top: true
---

> github的后端使用ruby，支持静态页面托管，也可以提交jekll源码，会自动生成静态页面，使用github提供的jekyll并不是必须需要本地安装jekyll的

# 安装ruby
<!-- more -->
jekyll是使用ruby语言开发的静态页面生成器，所以需要先安装ruby，在windows系统下访问[ruby的winsows官网](https://rubyinstaller.org/)找到最新版本下载包含开发包的ruby，安装，勾选将ruby添加到环境变量，安装结束后点击完成会弹出命令行，输入1回车，安装相关软件，结束后按回车退出，这样就安装了ruby环境，打开命令行输入`ruby -v`显示版本信息则说明安装没有问题

# 配置国内镜像

ruby类似python，js使用中往往需要下载依赖包，像python的`pip install` nodejs的`npm isntall`ruby也有自己的包管理器叫`gem`，由于网络环境的问题，配置国内镜像可以明显提高下载速度，方法如下

- 检查ruby版本 

```
gem -v # 建议为2.6及以上，第一步下载了最新版本这里一定满足条件
```

- 配置镜像

``` bash
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources -l
https://gems.ruby-china.com
# 确保只有 gems.ruby-china.com
```

> 附上[ruby中国](https://gems.ruby-china.com/)的官网

# 安装jekyll

一切都准备好了，安装jekyll

``` bash
gem install jekyll
```

# 本地预览

一般情况下，本地预览jekyll生成的网页需要这样的命令

``` bash
bundle install # 安装依赖，只有第一次运行需要
bundle exec  jekyll server # 启动本地服务器
```
访问localhost:4000

# 注意事项

使用jekyll时如果使用了主题，安装依赖时上面的镜像配置还不够，在用到Gemfile文件时，可以修改这个文件或者使用这个命令
``` bash
bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```