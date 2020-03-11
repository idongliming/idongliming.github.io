---
title: Github Action 实现 Hexo 自动部署
date: 2020-03-11 20:46:21
categories: 学习笔记 
tags: 
    - github
    - hexo
keywords: 
    - hexo
    - github action
    - 自动部署
top:   
cover: 
summary: 
password: 
mathjax: 
---

[GitHub Actions](https://help.github.com/en/articles/about-github-actions) 由 GitHub 官方的工作流工具。典型的应用场景应该是 CI/CD，类似 Travis 的用法。这里介绍响应 git push 事件触发 Hexo 编译静态页面并推送到 GitHub Pages 的用法。

### 准备工作

- 生成 ssh 部署私钥

    ```bash
    ssh-keygen -t ed25519 -f ~/.ssh/github-actions-deploy
    ```

- 在 GitHub repo 的 `Settings/Deploy keys` 中添加刚刚生成的公钥
- 在 GitHub repo 的 `Settings/Secrets` 中添加 `GH_ACTION_DEPLOY_KEY`，值为刚刚生成的私钥

也可以使用添加到github的密钥对**不需要**添加部署公钥只添加**私钥**到`Settings/Secrets`

### 编写 GitHub Actions

- 在项目的根目录添加 `deploy.yml`，目录结构如下

    ``` bash
    .github
    └── workflows
    └── deploy.yml
    ```

#### 步骤

- 添加部署私钥到 GitHub Actions 执行的容器中
- 在容器中安装 Hexo 以及相关的插件
- 克隆主题 [matery](git@github.com:blinkfox/hexo-theme-matery.git) 并覆盖默认配置
- 编译静态页面
- 推送编译好的文件到 GitHub Pages

- 编写部署的 action

```yaml
    name: Main workflow

on:
  push:
    branches:
    - source

jobs:
  build:
    runs-on: ubuntu-18.04
    steps:
    - uses: actions/checkout@v1
    - name: Use Node.js 10.x
      uses: actions/setup-node@v1
      with:
        node-version: '10.x'
    - name: prepare build env
      env:
        GH_ACTION_DEPLOY_KEY: ${{ secrets.GH_ACTION_DEPLOY_KEY }}
      run: |
        mkdir -p ~/.ssh/
        echo "$GH_ACTION_DEPLOY_KEY" > ~/.ssh/id_rsa
        chmod 600 ~/.ssh/id_rsa
        ssh-keyscan github.com >> ~/.ssh/known_hosts
        git config --global user.name 'idongliming'
        git config --global user.email 'idongliming@qq.com'
        npm i -g hexo-cli
        npm i
        git clone -b master git@github.com:blinkfox/hexo-theme-matery.git themes/matery
        cp source/_data/matery.yml themes/matery/_config.yml
    - name: deploy to github
      run: |
        hexo generate && hexo deploy

```

### 小结

使用github action 可以保证构建环境一致，临时更换电脑写博客不用搭建环境，装上git就可以写，这样的方式同样适用非专业的同学使用github搭建博客，用[github desktop](https://desktop.github.com/) clone项目编写发布即可

### 参考链接

- [Workflow syntax for GitHub Actions](https://help.github.com/en/articles/workflow-syntax-for-github-actions)
- [gythialy's blog](https://gythialy.github.io/deploy-hexo-to-github-pages-via-github-actions/)
