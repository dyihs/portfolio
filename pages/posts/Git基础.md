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

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150459.png)

当已经被添加到git暂存区的文件被修改后，使用如下命令将其添加到git暂存区：

```bash
git add -u
```

## 3、给文件重命名的简便方法  

###  方式一 

例如将使用 mv readme [readme.md](http://readme.md) 。命令将readme文件重命名为 [readme.md](http://readme.md)，然后使用 git status 命令查看状态，如图3-1所示，更改名称的过程是先将 readme 文件删除，然后创建了一个 readme.md文件。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150525.png)

在添加暂存区时，需要先使用提示信息的命令先先删除readme文件：  git rm readme  然后使用添加修改后的文件readme.md:  `git add readme.md ` 然后使用 `git status` 命令查看如下图 3-2 只有一条状态信息。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150548.png)

###  方式二  

相比于方式一，需要三个命令进行操作；方式二只需要下面一条命令，状态显示如 图 3-3。

```bash
git mv readme readme.md
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150607.png)

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

### 取消暂存区内容

```bash
git reset --hard # 直接将最新添加到暂存区的文件恢复并恢复工作目录更改的内容
git restore --staged # 将暂存区文件一步步恢复，但是不恢复工作目录的文件内容
```

## 4、通过 git log 查看版本演进历史

```bash
git log --oneline # 查看commit版本历史演进，只输出 message 信息
git log -n4 # 查看最近前4条记录
git log -n4 --oneline # 查看最近前4条信息的 message 信息

git branch -v # 查看本地有多少分支
git branch -av # 查看本地有多少分支
git checkout -b temp 7c02a5d203e8706 # 在 7c02a5d203e8706 节点上创建一个 temp 分支

git commit -am 'message' # 直接将文件提交，忽略暂存区，但是不推荐使用，使用下面两个命令
git add <file_name>
git commit -m 'message' # 

git log --all # 查看所有分支的提交的信息
git log --all --graph # 图形化提交信息
git log --all --oneline

# 查看commit版本记录组合命令
git log --all --oneline --graph -n4 
git log --all --oneline -n4

git log --oneline temp # 查看 temp 分支commit版本记录，但是不能使用 --all
```

 **下面的命令是查看git log 详细指令的命令**  

```bash
git help --web log
```

##  5 通过图形界面工具查看版本记录

mac系统在安装git之前是没有安装gui的，windows系统安装git时自带安装了gui。mac中需要单独使用下面命令安装 gui：brew install git-gui 。然后使用下面的命令打开图形化工具查看版本记录，如图5-1所示。

```bash
gitk
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150821.png) 

## 6 探秘 .git 目录

 如下图是.git目录内容。 

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150844.png) 

**HEAD**

 经常被使用的文件，cat HEAD 后内容是 ref: refs/heads/temp。ref是一个引用，指向redfs/heads/temp,表示HEAD指向temp这个分支，如果切换成main分支，里面内容是 ref: refs/heads/main。  

**config**

中包含了【core】和【user】信息，也就是于本地相关的配置信息。使用如下命令：

```bash
git config --local user.name 'sh'
```

然后再次查看config文件中【user】内容，发现 user.name=sh。

 **refs**

目录结构查看如下所示代码所示：

```bash
tree .git/refs
```

查看main文件内容，输出结果为308d3ad45d7715ef0e566a065bc95ad7cb7fc1c2，这表示main指向了一个commit，使用：

```bash
git log
```

 查看后发现main分支指向的commit操作是 308d3ad45d7715ef0e566a065bc95ad7cb7fc1c2 ，然后查看了 308d3ad45d7715ef0e566a065bc95ad7cb7fc1c2 类型是 commit  。

```bash
cat main
# 输出结果 ：308d3ad45d7715ef0e566a065bc95ad7cb7fc1c2
git cat-file -t 308d3ad45d7715ef0e566a065bc95ad7cb7fc1c2
# 输出结果：commit
```

 **tag** 

 ag中存放的是某个commit上打的标签，如下所示，这里的f0c5a1731e463f7bce63f60af8abb955dfc772a5 查看后类型是打标签的commit，输出的信息中也显示了 type commit，-p 后包含了该标签的详细信息，包括创建tag的说明。  

```bash
cat .git/refs/tags/js01
# 输出结果：751a55ec8e7f221934a7459775a31fdf7202992a
git cat-file -t 751a55ec8e7f221934a7459775a31fdf7202992a
# 输出结果：tag
git cat-file -p 751a55ec8e7f221934a7459775a31fdf7202992a
#输出结果：
#   type commit
#   tag js01
#		tagger shiyd shi.yaodong@foxmail.com 1674812353 +0800
#		the first js
git cat-file -t f0c5a1731e463f7bce63f60af8abb955dfc772a5
# 输出结果：commit
```

**object**

 如下图是object文件包含内容。  

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728150921.png)

里面包含了两个字符的文件夹，如下图所示，pack是将两个字符的文件打包后放入，进行自我梳理。如下所示，可以将 b3 这个文件与文件内容拼接后查看类型，包括commit、tree、blob类型，其中 tree 是一个目文件夹里面包含了 blob，blob 是一个文件。

- TODO：使用命令了解 b3 文件

## 7、分离头指针情况下注意事项

分离头指针是没有基于某个branch进行变更。如何在切换分支时不小心使用了commit id作为分支名称，就会出现分离头指针的情况，例如：  

```bash
git checkout 7c02a5d203e

上述代码输出结果：
注意：正在切换到 '7c02a5d203e'。 
您正处于分离头指针状态。您可以查看、做试验性的修改及提交，并且您可以在切换回一个分支时，丢弃在此状态下所做的提交而不对分支造成影响。
如果您想要通过创建分支来保留在此状态下所做的提交，您可以通过在 switch 命令中添加参数 -c 来实现（现在或稍后）。例如：

git switch -c <新分支名>
或者撤销此操作：
git switch -
通过将配置变量 advice.detachedHead 设置为 false 来关闭此建议
HEAD 目前位于 7c02a5d ADD styles.css
```

分离头指针是在没有分支的情况下工作，如果在该状态下commit了很多任务，但是在切换回main分支后分离头指针的commit记录会被git当垃圾清理掉，之前提交的任务就会消失。因为分离头指针没有与某个branch分支挂钩，所以在提交时需要与某个分支挂钩才会被清理。如下所示：

```bash
git checkout main
输出结果

警告：您正丢下 1 个提交，未和任何分支关联：

d5446b0 Background to green

如果您想要通过创建新分支保存它，这可能是一个好时候。 如下操作：

git branch <新分支名> d5446b0

切换到分支 'main'
```

在切换分支时会提醒为分离头指针的commit建立一个分支（git branch [新分支名] [分离头指针commit id]）分离头指针的好处是，在做实验性提交时，如果实验的并不理想，直接切换到分支就会自动清理掉之前的提交历史记录。但是如果发现分离头指针提交的内容重要，在切换分支后依然可以创建分支保存分离头指针的内容，然后查看git log，发现保存了分离头指针的内容。

## 8、进一步理解 HEAD和 branch

 可以基于分支创建一个分支，-b 表示创建好分支后直接切换到该分支，如下命令所示：  

```bash
git checkout -b fix-readme fix-css
切换到一个新分支 'fix-readme'
```

使用如下命令查看HEAD指向，发现HEAD指向了两个分支，分别是基于该分支和新分支。

```bash
git log -n1
# 输出结果：
commit d5446b0161ed178168808ea2838e7f9b03c15260 (HEAD -> fix-readme, fix-css)
Author: shiyd <shi.yaodong@foxmail.com>
Date:   Sat Jan 28 00:33:40 2023 +0800

    Background to green
```

 比较两个commit的差异，按 q 退出： 

```bash
git diff d5446b0161ed 7c02a5d203e8

git diff HEAD HEAD~1 # 当前HEAD指向的分支的commit与前一个commit比较
git diff HEAD HEAD^

git diff HEAD HEAD~2 # 当前HEAD指向的分支的commit与前两个commit比较
git diff HEAD HEAD^^
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230728151234.png)
