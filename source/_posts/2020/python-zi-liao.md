---
title: python资料
categories:
  - 学习笔记
tags:
  - 文档
toc: false
date: 2020-05-04 17:38:26
keywords:
top:
cover:
summary:
password:
mathjax:
---

python相关的学习资料总结索引

> 面向新手的笔记

# 基本语法

- [廖雪峰的python教程](https://www.liaoxuefeng.com/wiki/1016959663602400) ，比较接地气，通俗易懂，网页上可以直接执行代码
- [python官方网站](https://docs.python.org/zh-cn/3/) ，全面，具体，可以查自带模块的使用方法，有中文
- [菜鸟教程](https://www.runoob.com/python/python-tutorial.html) ，同样有在线工具，相比第一个，这个网站包含的教程比较多，都是语法和框架的

# 框架怎么学？

个人看法，先快速上手，再慢慢深入

## 上手

- [bilibli](https://www.bilibili.com/) 上看培训班传出的视频，环境搭建跟着做，架子搭起来
- 官网上的demo
- CSDN 博客园这类博客网站也可以找上手demo，分分钟可以体验一下某个框架 
- [github](https://www.github.com)搜`框架名字 demo`关键字一般都能找到一些简单入门的程序，星星多的项目一般项目结构也有参考价值

## 深入

- 官网文档
- 官方文档
- 官方文档

 **重要的说三遍，要想把一个框架学精，一定要把官网看完**，官网上的是出处，所有的教程都是从官网上学了以后加工的产物

- 做项目，按照一定的规范去写项目，去github找找有没有人写过某个项目开源了，参考优秀的项目架构，代码规范，任何语言都有代码规范检查工具，一定要用 `python` 有 `pylint` ,使用 [git](https://git-scm.com/)做版本控制

**github上资源很多，搜教程，搜书，搜代理软件，慢慢探索吧**

# 关于python依赖

在windows下安装多版本的 python 可以使用默认安装的 py 命令

## py

常用命令

- 列出安装的所有python版本 `py -0`
- 使用指定版本的python运行程序 `py -3.6 xx.py` 使用3.6版本运行xx.py文件
- 指定python版本的pip命令 比如用`py -3.6 -m pip` 代替pip命令使用python3.6安装模块

## Anacoda

使用anacoda管理多个版本的python，这个程序是创建虚拟环境用的不同的虚拟环境就像不同的隔离环境，在A环境安装的包在B虚拟环境中需要再次安装，适合电脑上有多个项目，不同项目依赖的包存在冲突时使用

常用命令

- 创建虚拟环境 `conda create --name 虚拟环境的名字 python=3.6` 创建了一个使用python3.6的虚拟环境
- 进入虚拟环境 `activate 虚拟环境的名字`
- 退出 `deactivate` 或者直接关掉终端（cmd）窗口

> 进入虚拟环境后可以使用pip安装需要用到的包，或者使用`conda install 包名` 命令安装需要的包
	**特殊情况下`import`时使用的的名字和安装时的名字不同**比如openCV，百度查一下某某包的安装命令

## pip 常用命令

- 安装一个包 `pip install 包名`
- 列出安装的包 `pip freeze` 这里输出的内容可以保存到文件里，方便在新电脑上安装 `pip freeze > requirements.txt`
- 批量安装包，读取前面保存的文件 `pip install -r requirements.txt` **注意：这里的文件名是一般用这个，但可以随便起名字 项目中打开是 包名==版本号 这样格式的文件是什么就从哪里安装**如果提示文件找不到，检查一下路径


> 补充 : git 使用[教程](https://git-scm.com/) 或者廖雪峰的git教程
	网络问题，从[这里](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/) 按照说明配置清华大学镜像，其他镜像源还有 豆瓣 阿里等，根据所在位置选择合适的镜像源