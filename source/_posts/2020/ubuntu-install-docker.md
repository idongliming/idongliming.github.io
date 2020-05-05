---
title: Ubuntu安装Docker
categories:
  - 后端
  - 学习笔记
tags:
  - docker
keywords: docker ubuntu install
top: ''
cover: ''
summary: ''
password: ''
mathjax: ''
toc: false
date: 2020-05-05 08:37:00
---

# 安装命令

``` bash
sudo apt-get install -y docker.io
```

等待安装完毕，现在我们使用下面的命令启动 Docker：

``` bash
systemctl start docker
```

运行系统引导时启用 docker，命令：

``` bash
systemctl enable docker
```