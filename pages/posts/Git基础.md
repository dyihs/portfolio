---
title: Git基础
date: 2018/3/19
description: Git基础
tag: Git基础
author: shiyd
---

## 1、使用Git之前需要的最小配置

配置User信息：

配置user.name和user.email；在提交代码时，需要带上相关提交人的信息，没有配置，会有相关的提示信息。

```bash
git config --global user.name 'your_name'
git config --global user.email 'your_email'
```

config的三个作用域：

**优先级：local>global>system**

缺省作用域等同于local；local只针对某个仓库有效、global对当前用户所有仓库有效、system对系统所有登录的用户有效。

```bash
git config --local
git config --global
git config --system
```

显示config某个作用域的配置加 ——list

```bash
git config --list --local
git config --list --global
git config --list --system
```

**Git配置命令：**

```bash
git config --local user.name 'your_name' # local 域配置信息
git config --local user.email 'your_email'

git config --global user.name 'your_name' # global 域配置信息
git config --global user.email 'your_email'

git config --system user.name 'your_name' # system 域配置信息
git config --system user.email 'your_email'

git config --local --list # 查看配置信息
```

## 2、建立Git仓库

两种场景：

（1）把已有的项目代码纳入Git管理。

```bash
cd 项目代码所在文件夹
git init
```

（2）新建项目直接使用Git管理。

```bash
cd 某个文件夹
git init your_project # 会在当前文件夹下创建项目同名的文件夹
cd your_project
```

（3）示例：

```bash
git init git-practise
cd git-practise
git branch -m main # git 默认分支是master，github仓库使用的是main，切换成main
git config --global --list # 查看git global作用域的配置信息
git config --local user.name 'shiyd' #设置local作用域的user.name
git config --local user.email 'shiyd@foxmail.com' # 设置local作用域的user.email
git config --local --list # 查看配置信息
```

想当前git仓库添加一个readme的文件，然后执行:`git commit -m 'ADD readme'`

会出现如图2-1的提示信息，表示改文件没有被添加到git仓库管理。需要执行提示上面的命令：

```bash
git add readme 
```

然后执行:

```bash
git status
```

查看git现在的状态，显示文件颜色为绿色表示文件在git管理的范围，如图2-1。

![img](https://cdn.nlark.com/yuque/0/2023/png/12871800/1689233488884-ac2bc166-f74a-4eb9-a325-b1125567a4ab.png)
