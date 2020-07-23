---
title: hexo 工具
categories:
  - 学习笔记
tags:
  - 工具
keywords: hexo vscode 工具

date: 2020-05-04 16:32:35
updated: 2020-07-23 18:31:30
---

# hexo client

专为hexo打造的客户端，使用体验：

- 传图片方便了很多
- 标签分类也能可视化的选择或添加新的
- 编辑foront-matter方便很多🤣
- 编辑md文件可以可视化，增加一种新的选择，尤其编辑表格，会有优势
- 一键发布，不用写命令了，支持github action和原生的hexo g -d

## 下载地址

[hexo client](https://github.com/gaoyoubo/hexo-client)

# vscode + hexo utils

- 启动比 hexo client 快
- 传图片方便
- 可以创建管理文章

- 配合简单的node脚本方便快捷

## 下载地址

[vscode hexo utils](https://github.com/cwxyz007/vscode-hexo-utils/)

## 我的配置

```json
"scripts": {
    "test": "hexo clean && hexo generate && hexo server",
    "pull": "git pull origin source",
    "push": "git add . && git commit -m\"add a post\" && git push origin source"
  }
```