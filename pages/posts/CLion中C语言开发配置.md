---
title: CLion中C语言环境配置
date: 2019/1/11
description: CLion中C语言环境配置
tag: C
author: shiyd
---

### 所需工具

1. MinGW：官网下载地址 https://www.msys2.org/ ，安装MinGW是为了方便管理开发工具，比如有GCC和编译器等开发工具。打开安装目录选择 msys2.exe 运行，`pacman -Su`  命令更新资源包，`pacman -Sy base-devel` 安装基础大包 。`pacman -S mingw-w64-x86_64-toolchain` 命令安装MinGW工具链。

2. Visual Studio 2022：Windows系统下开发所需要的工具。
3. CLion：IDE开发工具，在该工具中的setting中构建、执行、部署，如下图所示包含了WSL、Windows和MinGW工具链。

![图1-1 CLion 配置](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230629165519.png)

### 关于DEBUG：

如果使用的是MinGW，则是GCC编译器，在DEBUG后编译使用的是GDB，GDB模式有 att 和 intel，默认使用的是att，使用 `set disassembly-flavor intel` 命令更改 为intel，如果长久使用intel模式，则在 `c\\user\\username` 目录下建立一个 .gdbinit 文件，将更改的命令添加进去。

如果使用的MSVC编译器则是LLDB，默认使用的是att，使用  `setting set target.x86-disassembly-flavor intel` 命令更改 为intel，如果长久使用intel模式，则在 `c\\user\\username` 目录下建立一个 .lldbinit文件，将更改的命令添加进去。

### 解决CLion中只执行一个main函数的程序

将 CMakeLists.txt 内容改写成如下内容可以执行每个程序：

```makefile
cmake_minimum_required(VERSION 3.26)

get_filename_component(ProjectId ${CMAKE_CURRENT_SOURCE_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId})
project(${ProjectId} C)

set(CMAKE_C_STANDARD 11)

# 添加当前文件夹 （CMakeLists.txt 所在文件夹）的 *.c 文件
#file(GLOB files "${CMAKE_CURRENT_SOURCE_DIR}/*.c")

# 添加 sort 文件夹的 *.c 文件
#file(GLOB sort "${CMAKE_CURRENT_SOURCE_DIR}/sort/*.c")

# 将所有 *.c 文件合并成一个列表
#list(APPEND all_files ${files} ${sort})

# 不推荐使用 file(GLOB ...) 命令，手动列出源文件
#set(SOURCE_FILES
#        ${CMAKE_CURRENT_SOURCE_DIR}/main.c
#        ${CMAKE_CURRENT_SOURCE_DIR}/sort/sort.c
#        # 添加其他源文件，如果有的话
#)

# 使用 file(GLOB ...) 命令获取源文件列表
file(GLOB SOURCE_FILES
        "${CMAKE_CURRENT_SOURCE_DIR}/*.c"
        "${CMAKE_CURRENT_SOURCE_DIR}/sort/*.c"
)

foreach (file ${SOURCE_FILES})
    get_filename_component(name ${file} NAME)
    add_executable(${name} ${file})
endforeach ()
```



