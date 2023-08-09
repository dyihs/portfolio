---
title: C51 Keil 环境搭建
date: 2017/11/7
description: C51 Keil 环境搭建
tag: 嵌入式
author: shiyd
---

[TOC]
### 配置 C51 版本 Keil 环境

下载 STC8 烧录软件：https://www.stcmcudata.com/ ，打开之后选择芯片型号为 STC8H8K64U 然后选择“Keil仿真设置”，点击添加头文件到 Keil中，选择 Keil 的第一层安装目录，确定后则会添加成功，在 Keil 安装目录 Keil_v5\C51\INC\STC 中会显示 STC8H8 的头文件。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706174011.png)

到 Keil 官网下载 C51 开发软件，主要用于 8051 开发。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706173422.png)

打开 Keil 软件，设置中文环境下乱码情况，如下图所示，在 Edit->Configuration 中 Encoding 中选择 Chinese GB2312。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706173806.png)

### 创建项目

打开 Keil 点击 Project 菜单创建项目，如下图 2-1 所示，每个项目有单独的文件包，在该文件包中创建一个项目文件。如下图 2-2 选择需要添加的待开发芯片的头文件。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706174725.png)

​			图 1-1 创建项目

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706175209.png)

​			图 1-2 添加开发STC的头文件

### 编译项目并点灯测试

在编译程序之前，需要在 Keil 中创建烧录程序，如下图 3-1 所示打开创建烧录程序（HEX）的界面。选择 OUTPUT ，勾选 Create HEX File，如下图 3-2。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706191001.png)

​				图 3-1 打开烧录程序



![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230706232109.png)

​				图 3-2 创建 HEX 文件

### AStyle格式化工具

在 Keil IDE中的`Tools`目录下选择 `Customize Tools Menu` ，添加格式化当前文件命令，如下图所示；

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230722205644.png)

AStyle 的格式化命令可以参考该链接的文章 https://www.cnblogs.com/RioTian/p/14771895.html 

