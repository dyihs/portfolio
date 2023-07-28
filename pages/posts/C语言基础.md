---
title: C语言基础
date: 2017/9/23
description: C语言基础
tag: C
author: shiyd
---

### 数据类型

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230629182223.png)

除了上图中数据类型外，基本类型中整型还有 `long int` 、 `long long`  ，浮点型类型还有 `long double`

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230630174230.png)

数据类型长度和单位：

1. bit(比特)

   一个二进制代表一位，一个位只能表示0或1两种状态。数据传输是习惯以“位”（bit）为单位。

2. Byte(字节)

   一个字节为8个二进制，称为8位，计算机中存储的最小单位是字节。数据存储是习惯以“字节”（Byte）为单位。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230630172757.png)

可移值类型：

C语言程序在移植过程中可能会出现不同平台数据类型不兼容，为了解决这个问题，C语言在可移植类型 stdint.h 和 inttype.h 中规定了精确宽度整数类型，以确保C语言的类型在各系统内功能相同。

```
#include <stdio.h>
#include <inttypes.h>

int main()
{
		int8_t x1 = 32;
		int16_t x2 = 42;
		
		// unsigned 无符号，没有符号位，数值为正数
		uint8_t ux = 235;
		uint16_t ux1 = 323;
}
```

#### char 类型：

- 字符型变量用于存储一个单一字符，在 C 语言中每个字符变量都会占用 1 个字节。
- 在给字符型变量赋值时，需要用一对英文半角格式的单引号(' ')把字符括起来。
- 字符变量实际上并不是把该字符本身放到变量的内存单元中去，而是将该字符对应的ASCII码放到变量的存储单元中。
- char的本质就是一个1字节大小的整型。

主要记住下面几个ASCII值，大写字母与小写字母相差32：

| 控制字符 | ASCII值 |
| :------: | :-----: |
|    0     |   48    |
|    A     |   65    |
|    a     |   97    |



### 字面量添加后缀

不同进制

- 二进制：0b11。
- 八进制：011。
- 十六进制：0x11。

给字面量添加后缀表明类型。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230630174616.png)

或使用 `stdint.h` 内定义宏。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230630174721.png)



### 格式化站位符

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230630174848.png)



### 标识符

规则说明：

- 由数字, 字母, 下划线_组成
- 不能使用数字开头
- 不能使用关键字
- 严格区分大小写

关键字：

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230629181923.png)

命令规范：

好的命名习惯要做到见名知意

- 大驼峰

- - 每个单词首字母大写, 例如: MyFirstName

- 小驼峰

- - 第二个单词开始首字母大写, 例如: myFirstName

- 下划线命名

- - 每个单词之间使用下划线连接, 例如: my_first_name



### 变量和常量

变量（值可变）：

```c
int x;			// 未初始化的变量，值可改变
int xx = 19;	// 初始化后的变量，值也可改变
printf("x = %d, xx = %d\n", x, xx);	// 输出 x = 0, xx = 19
```

常量（值不可变）：

```c
#include <stdio.h>
// 预处理常量
#define PI 3.14

int main()
{
    	// const 常量
		const double pi = PI;
    	printf("pi = %.2f, PI = %.2f\n", pi, PI);
}
```

除此之外还有系统常量，如下图所示：

1. float.h

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230629181219.png)

2. limits.h

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230629181159.png)



### 参考

[1] C程序设计笔记：https://www.yuque.com/qyuhen/c11/vfl3hq

[2] 网道C语言教程：https://wangdoc.com/clang/types