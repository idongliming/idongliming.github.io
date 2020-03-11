---
title: git代理
tags:
  - git
categories: 学习笔记
date: 2019-06-09 13:26:13
---
访问github处理较大的仓库时速度有些慢，可以设置socket代理。访问国内git托管平台时取消

github上的[讨论](https://gist.github.com/laispace/666dd7b27e9116faece6)
<!-- more -->
- 设置http方式的代理

``` bash
git config --global http.proxy 'socks5://127.0.0.1:1080'
```

- 取消代理

``` bash
git config --global --unset http.proxy
```

- ssh方式的代理

在~/.ssh/config 文件后面添加几行，没有可以新建一个

```
# 这里必须是 github.com，因为这个跟我们 clone 代码时的链接有关
Host github.com
   # 如果用默认端口，这里是 github.com，如果想用443端口，这里就是 ssh.github.com 详见 https://help.github.com/articles/using-ssh-over-the-https-port/
   HostName github.com
   User git
   # 如果是 HTTP 代理，把下面这行取消注释，并把 proxyport 改成自己的 http 代理的端口
   # ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=6667
   # 如果是 socks5 代理，则把下面这行取消注释，并把 6666 改成自己 socks5 代理的端口
   ProxyCommand connect -H 127.0.0.1:1080 %h 22

```