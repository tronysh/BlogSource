---
title: 个人博客的搭建和配置
date: 2019-10-19 07:55:01
tags: 
- Blog
- 教程
- Github
categories:
- 博客搭建
description: 
---

本博客搭建参考了以下几篇文章：

[使用GitHub/GitLab/码云搭建个人博客](https://dp2px.com/2017/11/15/hexonext/)

这篇文章介绍得非常详细，有兴趣可以参考一下。
<!-- more -->
[使用next主题](http://theme-next.iissnan.com/getting-started.html)

这里使用next的版本已经停止维护了，建议使用最新版本 [next](https://theme-next.org/docs/getting-started/)

[为NexT主题添加文章阅读量统计功能](https://notes.doublemine.me/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)

这个在 [next](https://theme-next.org/docs/getting-started/) 的doc里都有介绍
___

## 安装 [nodejs](https://nodejs.org/en/)

安装完后打开cmd，这里我用的是powershell，输入`npm -v`

## 安装 [Git](https://git-scm.com/download/win)

安装完成后打开Git Bash，输入

```
git config --global user.name "username" //Github的用户名
git config --global user.email "email" //Github的邮箱
```

## 配置本地SSH

```
ssh-key -t rsa -C "email"      //此处“C”要大写，邮箱使用Github注册邮箱
```
之后一路回车过去即可

### 将SSH配置到Github

生成ssh-key后会提示保存的路径，用文本编辑器打开文件，复制文件内所有文本。打开Github，在设置里的SSH里添加我们自己的ssh-key。

## 安装hexo

```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```

这时候如果没问题的话，可以在[本地服务器](http://localhost:4000/)看到自己的博客了。

## 在Github上新建一个公共项目

名字为 `username.github.io` ，必须是这个格式

## 修改_config.yml

将repo的url改成自己项目的地址，这样在后面deploy时就会上传到github的项目里。
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git

  branch: master
```

## 部署到Github

```
npm install hexo-deployer-git --save
```
然后 输入命令

```
hexo d
```

这时候可以到自己项目里看一下，发现public里的文件都上传到Github了。

## 使用免费域名

在Github你的项目设置里Github Pages前勾上

这时候可以通过` https://username.github.io `访问你的博客了

## 更新博客

之后在更新博客时，我们只需要

```
hexo g
hexo d
```
## 配置域名

我们可以在阿里云查询自己想要的域名，一般冷门域名首年比较便宜，购买后经过域名实名审核，我们就可以在域名管理器里配置我们的域名了。

首先自己先ping一下自己的博客网站

```
ping username.github.io
```
然后将得到的ip复制，在域名管理器里我们编辑解析设置。记录类型选择 ` A-将域名指向一个ipv4地址`，主机记录填`@`，解析线路选择默认就好了，记录值填自己刚才复制的ip地址。

然后我们在github的项目设置里，将github page的domain填上自己申请的域名，就可以通过自己的域名访问博客了。

