---
title: 重装系统后hexo博客恢复
date: 2020-02-13 16:24:19
tags:
- Blog
- 教程
categories: 
- 博客搭建
description: 系统重装后，如何重新部署hexo+github搭建的博客。
---

### 安装Git和Node.js

[Git下载](https://git-scm.com/)
[Node.js下载](https://nodejs.org/en/)

配置Git和Node.js环境变量

### 配置git个人信息，生成新的ssh密钥

```
git config --global user.name "xxxxxx"
git config --global user.email "xxxxxx"
ssh-keygen -t rsa -C "xxxxxxxx(邮箱)"
```

### 添加公钥

把.ssh文件里面的公钥复制出来粘贴到GitHub个人设置中的ssh

### 删除部分文件

打开原来博客的文件夹，除了_config.yml，theme/，source/，scaffolds/，package.json，.gitignore，其余删掉

### 运行npm

打开powershell输入`npm install`

`npm install hexo –save`

### 安装部署文件

`npm install hexo-deployer-git --save`

### 调试

```
hexo clean
hexo g
hexo d
```