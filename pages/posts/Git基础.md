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

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150041.png)

### 建立仓库命令：  

```bash
git add <filename> # 将文件添加到暂存区
git commit -m '<message>' # 提交文件，并说明（message）
git log # 查看提交的信息
git log --graph # 查看提交的信息，线条式显示 
```

 图2-2 是git管理过程 。

![](https://cdn.nlark.com/yuque/0/2023/png/12871800/1689233578222-f3eb0adb-42c6-4f9f-8983-f3ffb1678a13.png)

当已经被添加到git暂存区的文件被修改后，使用如下命令将其添加到git暂存区：

```bash
git add -u
```

##  3 给文件重命名的简便方法  

###  方式一 

例如将使用 mv readme [readme.md](http://readme.md) 。命令将readme文件重命名为 [readme.md](http://readme.md)，然后使用 git status 命令查看状态，如图3-1所示，更改名称的过程是先将 readme 文件删除，然后创建了一个 readme.md文件。

![](https://cdn.nlark.com/yuque/0/2023/png/12871800/1689233697153-3bc4c1ac-a01c-4b32-9572-00e41899f3d9.png)

在添加暂存区时，需要先使用提示信息的命令先先删除readme文件：  git rm readme  然后使用添加修改后的文件readme.md:  `git add readme.md ` 然后使用 `git status` 命令查看如下图 3-2 只有一条状态信息。

![](https://cdn.nlark.com/yuque/0/2023/png/12871800/1689233848391-c0cfe1c4-de9f-4f82-8e02-f31d294858d5.png)

###  方式二  

相比于方式一，需要三个命令进行操作；方式二只需要下面一条命令，状态显示如 图 3-3。

```bash
git mv readme readme.md
```

![img](https://cdn.nlark.com/yuque/0/2023/png/12871800/1689237003994-2e51127d-f5e1-4e9b-8ead-f6ba3d3a43d7.png)

**拓展：**

```bash
git rest --hard
```

上面的命令是将最新添加到暂存区的文件撤回并将工作目录的文件恢复，因此这个命令会将 git add 后的工作目录文件信息恢复原样，之前做过修改的文件内容会丢失，因此是个相当危险的操作。可以使用:

```bash
git restore --staged <file_name>
```

这个命令将暂存区的文件取消，但是不会删除工作目录被更改的文件内容。例如：

```bash
git reset --hard
git restore --staged readme readme.md # 代替 git reset --hard 命令
```

###  更改文件名命令

```bash
mv readme readme.md # 将文件readme更改为readme.md
git rm readme # 在将文件添加到暂存区之前需要先删除readme
git add readme.md

git mv readme readme.md # 直接更改文件readme 为 readme.me 并添加到暂存区
```

###  取消暂存区内容
