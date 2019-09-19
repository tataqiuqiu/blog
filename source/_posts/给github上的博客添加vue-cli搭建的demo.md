---
title: 给github上的博客添加vue-cli搭建的demo
date: 2019-8-5 19:00:00
tags: vue-cli
categories:
  - javascript
  - vue
  - vue-cli
---

记录一下这个blog添加demo的过程

## 一、创建一个新的github仓库。

### 1、创建库，起名demos

![](/images/github新建库.png)

<!-- more -->

### 2、打开settings

![](/images/github-settings.png)

### 3、启用GitHub Pages

![](/images/github开启pages.png)

## 二、gitignore文件中 去掉/dist目录

## 三、vue-cli3 路径配置

### 1、vue.config.js配置文件中的baseUrl改为相对路径。

bulid后的文件静态资源引用就会以相对路径来引入了。
包括外链JS、css以及，html内的img标签。

![](/images/vuecli3-config-baseurl.png)

### 2、router路径更改

将base改为目标路径，跳转路由的位置就会以此为根目录进行跳转。

![](/images/vuecli3-router-base.png)
