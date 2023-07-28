---
title: C语言数组
date: 2017/9/27
description: C语言数组
tag: C
author: shiyd
---

### 数组的使用

定义语法格式：类型 数组名[元素个数]；数组名不能与其他变量名相同，同一作用域内是唯一的，下标是从 0 开始计算。

### 可变长度的数组

可变长度数组就是使用 非常量表达式来定义数组，该数组具有自动生存周期，如下代码所示：

```c
void array_variable_length(int n)
{
        int array[n];
        for (int i = 0; i < n; i++) {
            	// 使用下标进行初始化
                array[i] = i;
        }
        printf("%d\n", sizeof(array) / sizeof(array[0]));
}
int main()
{
        printf("%d\n", sizeof(x) / sizeof(x[0]));
        array_variable_length(2);
        return 0;
}
```

### 下标存储和初始化

- 在定义数组的同时赋值，称为初始化。
- 全局数组若不初始化，编译器将其初始化为零。
- 局部数组若不初始化，内容为随机值。

```c
int a1[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 }; // 定义一个数组，同时初始化所有成员变量
int a2[10] = { 1, 2, 3 }; // 初始化前三个成员，后面所有元素都设置为0
int a3[10] = { 0 }; // 所有的成员都设置为0

// []中不定义元素个数，定义时必须初始化
int a4[] = { 1, 2, 3, 4, 5 }; // 定义了一个数组，有5个成员
```

数组名是一个地址的常量，代表数组中首元素的地址，所以当取数组中元素时，使用数组名称带下标获取元素是不是也就相当于一个指针变量获取地址中的元素一样，因此 **(array + i) 表示 array[i]（下标为1的元素），* * 和 [] 是一样的作用，操作指针指向内存空间，如下代码所示：

```c
#include <stdio.h>

int main()
{
        // * 和 [] 是一样的作用，操作指针所指向的空间
        int array[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

        int len = sizeof(array) / sizeof(array[0]);

        for (int i = 0; i < len; i++) {
                // printf("%d ", array[i]);
                printf("%d ", *(array + i));
        }
        printf("\n");

        // 定义一个指针变量，保存首元素地址
        int *p;
        p = array; // p = &array[0]
        for (int i = 0; i < len; i++) {
                // printf("%d ", *(p + i));
                printf("%d ", p[i]);
        }
        printf("\n");

        return 0;
}
```

C 不会进行越界检查，也就是不会对数组下标索引进行范围检查，因此C中只有可变长度数组。数组名默认是指向第一个元素指针的常量，而 &array[i] 则返回 int* 类型指针，指向目标元素的地址。

C中初始化方式。除了使用下标初始化外，还可以直接用初始化器。

```c
int array[] = {1, 2, 3};	// 不提供长度初始化器
int array2[5] = {1, 2};		// 提供长度和初始化器
int z[][2] = {{1, 1},{2, 1},{3, 1}};
```

初始化特定的元素：

```c
int array[] = {1,2,[6]=10,11};
int len = sizeof(x) / sizeof(int);

for (int i = 0; i < len; i++){
    printf("array[%d] = %d\n", i, array[i]);
}

输出：
array[0] = 1
array[1] = 2
array[2] = 0
array[3] = 0
array[4] = 0
array[5] = 0
array[6] = 10
array[7] = 11
```

### 指针数组

指针数组，也就是数组是指针类型（int *array[5]），数组的每个元素都是指针类型，存储元素是内存地址。

```c
#include <stdio.h>

int main()
{
    	int *array[3];
    	
    	int a = 1;
        int b = 2;
        int c = 3;

        // 赋值时，只能赋值变量的地址，指针变量赋值
        p[0] = &a;
        p[1] = &b;
        p[2] = &c;

        for (int i = 0; i < sizeof(p) / sizeof(p[0]); i++) {
                printf("%d, ", *(*(p + i)));
                // printf("%d, ", *(p[i]));
        }
        printf("\n");

        return 0;
    	
}
```

### 数组名做函数参数

数组名做函数参数，函数的形参本质上就是指针，未初始化大小的数组作为函数参数，此时需要给函数再添加一个参数，表示一个数组的长度。

```c
#include <stdio.h>

// 未初始化大小的数组作为函数参数需要添加一个参数，表示一个数组的长度
void parameter_array(int array[], int len)
{
        for (int i = 0; i < len; i++) {
                printf("%d ", array[i]);
        }
}

// 数组名作为参数，函数形参本质上就是指针
void parameter_array_pointer(int *array, int len)
{
        for (int i = 0; i < len; i++) {
                printf("%d ", array[i]);
        }
}

int main()
{
        int array[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int len = sizeof(array) / sizeof(int);
        variable_array(array, len);

        return 0;   
}
```

### 字符数组和字符串

C语言中没有字符串这种数据类型，可以通过 char 的字符数组来替代，数字 0 (和字符 \0 等价)结尾的 char 数组就是一个字符串，字符串是一种特殊的 char 的数组。以 \0 结尾的字符数组是字符串，有 '\0' 的数组其后面的元素不会输出。

字符是单引号括起来的字符类型，只有一个字符，字符串是双引号括起来的多个字符，其中最后一位是 \0 ，因为编译器会自动在后面补 0。

```c
#include <stdio.h>

int main()
{
        // 普通字符数组，没有 '\0' 结束符
        char str[] = {'h', 'e', 'l', 'l', 'o'};
        // 有可能乱序输出，数组输出时无序的
        printf("str = %s\n", str);

        // 以 \0 结尾的字符数组是字符串，
        char str1[] = {'h', 'e', 'l', 'l', 'o', '\0'};
        printf("str1 = %s\n", str1);

        // 有 '\0' 的数组其后面的元素不会输出
        char str2[] = {'h', 'e', 'l', 'l', 'o', 'w', '\0', 'w', 'o', 'r', 'l', 'd', '\0'};
        printf("str2 = %s\n", str2);

        // 使用字符串初始化，编译器自动在后面补 0，
        char str3[] = "hello";
        printf("str3 = %s\n", str3);

        // 普通字符串和字符数组的区别
        char str4 = 'a';                // 单引号，是字符类型，只有一个字符
        char str5[] = "a";              // 双引号，是合法的字符一组，有两两字符，最后一个是 \0

        printf("str4 = %c\n", str4);
        printf("str5 = %s\n", str5);

        return 0;
}
```

### 字符指针

字符指针可直接赋值为字符串，保存的实际上是字符串的首地址，和之前提到的数组和指针数组等价，* 和 [] 是一样的作用，操作指针指向内存空间。

```c
#include <stdio.h>

int main()
{
        // 定义一个字符指针
        // char *p = "hello" 省略了 const ，const char *p = "hello", 有没有 const 都一样
        // const 靠近 *p，因此 *p 不能修改， p 可以修改
        char *p = "hello";

        // *p = "a";
        printf("p = %s\n", p);

        p = "world";

        printf("p = %s\n", p);

}
```

### 字符串常用库函数

1. strlen

size_t strlen(const char *s);功能：计算指定指定字符串s的长度，不包含字符串结束符‘\0’。参数：s：字符串首地址；返回值：字符串 s 的长度，size_t 为 unsigned int类型，不同平台会不一样

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[] = "hello world";
    int len = strlen(str);
    printf("len = %d\n", len);

    return 0;
}
```

2. strcpy

char *strcpy(char *dest, const char *src); 功能：把src所指向的字符串复制到dest所指向的空间中，'\0'也会拷贝过去。参数：dest：目的字符串首地址，如果参数dest所指的内存空间不够大，可能会造成缓冲溢出的错误情况，src：源字符首地址；返回值成功则返回dest字符串的首地址，失败返回NULL。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char dest[20] = "123456789";
    char src[] = "hello world";
    strcpy(dest, src);
    printf("%s\n", dest);

    return 0;
}
```

3. strcat

char *strcat(char *dest, const char *src);功能：将src字符串连接到dest的尾部，‘\0’也会追加过去，参数 dest：目的字符串首地址，src：源字符首地址；返回值成功，返回dest字符串的首地址，失败为NULL。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str[20] = "123";
    char *src = "hello world";
    strcat(str, src);
    printf("%s\n", str);

    return 0;
}
```

4. strcmp

int strcmp(const char *s1, const char *s2)；功能：比较 s1 和 s2 的大小，比较的是字符ASCII码大小。参数 s1：字符串1首地址，s2：字符串 2 首地址。返回值相等：0 ，大于：> 0 ，小于：< 0。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char *str1 = "hello world";
    char *str2 = "hello mike";

    if (strcmp(str1, str2) == 0) {
        printf("str1==str2\n");
    } else if (strcmp(str1, str2) > 0) {
        printf("str1>str2\n");
    } else {
        printf("str1<str2\n");
    }

    return 0;
}
```

**注意：**

在C语言中，数组可以越界查询，因为C语言在进行数组访问时没有进行越界检查。C语言的设计初衷是提供高性能和灵活性，为程序员提供更大的控制权，而不是过多地增加运行时的开销和检查。

当对数组进行越界访问时，C语言并不会提供任何保护机制或警告。这可能导致访问到未分配的内存区域或其他变量的存储空间，造成不可预测的行为，例如程序崩溃、数据损坏或安全漏洞等。

因此，在编写C语言代码时，应该特别注意避免数组越界访问。可以通过合理的编程习惯和代码设计来防止这种情况的发生，例如使用循环结构控制数组的访问范围、使用条件语句检查索引的合法性，或者使用辅助函数和库来处理数组的操作。

同时，现代的编译器和调试工具通常会提供一些警告和调试信息，可以帮助您发现和修复数组越界访问的问题。因此，在开发过程中，建议使用优秀的工具和技术来帮助检测和排查此类问题。

