---
title: 关于跨域
tags:
  - cross
categories: 学习笔记
date: 2019-03-21 13:26:13
---
浏览器为了安全，只有同一域名，同一端口才会被允许，否则就要被禁止
<!--more-->

# 如何配置

配置允许跨域既要在前端配置，又要在后端配置才能正确访问
<!-- more -->
## 前端

- vue

``` js
proxyTable: {
      '/api': {
        target: 'http://localhost:5000',//后端接口地址
        changeOrigin: true,//是否允许跨越
        pathRewrite: {
            '^/api': '',// 使用/api代表target的值
        }
      }
    }

```

## 后端

- spring boot 跨域 @CrossOrigin注解
- flask 
``` python
rom flask_cors import CORS

app = Flask(__name__)
CORS(app, supports_credentials=True)
```