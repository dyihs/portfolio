---
title: 隐藏在Python的CLI工具
date: 2018/5/10
description: 隐藏在Python的CLI工具
tag: Python
author: shiyd
---

## 1. 使用 Python的gzip模块解压缩

```python
python -m gzip --decompress pypi.db.gz
```

如果 Windows 中没有安装 gzip 实用工具，可以使用该命令进行解压，如下图所示，使用该命令加压后的文件。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804143617.png)

## 2. 查看标准库位置

```python
python -m site
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804143709.png)

`python -m site` 这个命令的主要功能是查看 Python 解释器的模块搜索路径和安装位置信息。

具体来说：

1.  `python`: 这是在命令行中运行 Python 解释器的命令。 
2.  `-m`: 这是 Python 解释器的一个选项，表示要加载一个模块进行运行。 
3.  `site`: 这是要加载的模块的名称，即 `site` 模块。 

当执行这个命令后，Python 解释器会加载 `site` 模块，并执行其中的代码。`site` 是 Python 的标准库中提供的一个模块，主要用于处理模块搜索路径和模块安装位置的相关信息。

通过运行这个命令，你可以查看 Python 解释器中的模块搜索路径、默认的安装位置以及其他与模块管理相关的信息。这对于理解 Python 模块的导入机制、查找模块文件的规则等很有帮助。

## 3. 使用 Python的http.serer模块分享本地资源

在需要分享的目录下，按住 shift 右击选择 powershell 或者 cmd，输入如下命令，第一条没有指定端口，默认是8000端口，第二条指定80端口，可以不输入端口直接访问。

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804143745.png)

## 4. base64

```python
python3.11 -m base64 -h
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804143926.png)

## 5. 开启异步Python控制台

```python
python -m asyncio
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144001.png)

`python -m asyncio` 这个命令的主要功能是运行 Python 解释器，并加载 `asyncio` 模块。

当执行这个命令后，Python 解释器会加载 `asyncio` 模块，并执行其中的代码。`asyncio` 是 Python 的标准库中提供的一个模块，用于支持异步编程。

通过运行这个命令，你可以在命令行中使用 `asyncio` 模块提供的功能，例如创建异步任务、使用协程（coroutine）进行异步编程、处理异步事件循环等。异步编程是一种高效的编程方式，特别适用于处理 I/O 密集型任务和网络编程。在运行这个命令后，你可以尝试使用 `asyncio` 模块来体验 Python 的异步编程特性。

## 6. tokenize(标记)

```python
python -m tokenize cgi.py | head -n 10
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144228.png)

这个命令的主要功能是对名为 `cgi.py` 的 Python 脚本文件进行词法分析，并显示其前10个词法标记。

具体来说：

1.  `python -m tokenize`: 这部分是在命令行中运行 Python 解释器，并加载 `tokenize` 模块。`-m` 参数表示要运行一个模块，后面紧跟着模块的名称。 
2.  `cgi.py`: 这是要进行词法分析的 Python 脚本文件的名称，即 `cgi.py`。 
3.  `|`: 这是 Linux/Unix 系统中的管道符号，用于将前一个命令的输出作为后一个命令的输入。 
4.  `head -n 10`: 这部分是将 `tokenize` 模块的输出通过管道传递给 `head` 命令。`head` 命令用于显示文件的前几行，默认显示前10行（因为 `-n 10` 表示显示前10行）。 

综合起来，这个命令的作用是：运行 Python 解释器，对 `cgi.py` 文件进行词法分析，然后将其词法标记的前10个显示在终端上。这样可以查看 `cgi.py` 文件的词法结构，即将其拆分成单个的词法标记（例如标识符、关键字、运算符、字符串等），以了解其构成和语法。可直接针对文件运行，查看分词的内容：

## 7. AST模式（抽象语法树）

与tokenize相比，AST 模式如下：

```python
python -m ast cgi.py | head -n 10
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144316.png)

这个命令的主要功能是对名为 `cgi.py` 的 Python 脚本文件进行语法分析，并显示其抽象语法树（AST）的前 10 行。具体来说：

1.  `python -m ast`: 这部分是在命令行中运行 Python 解释器，并加载 `ast` 模块。`-m` 参数表示要运行一个模块，后面紧跟着模块的名称。 
2.  `cgi.py`: 这是要分析的 Python 脚本文件的名称，即 `cgi.py`。 
3.  `|`: 这是 Linux/Unix 系统中的管道符号，用于将前一个命令的输出作为后一个命令的输入。 
4.  `head -n 10`: 这部分是将 `ast` 模块的输出通过管道传递给 `head` 命令。`head` 命令用于显示文件的前几行，默认显示前10行（因为 `-n 10` 表示显示前10行）。 

综合起来，这个命令的作用是：运行 Python 解释器，对 `cgi.py` 文件进行语法分析，然后将其抽象语法树的前 10 行显示在终端上。这样可以查看 `cgi.py` 文件的抽象语法树的部分内容，以了解其语法结构和组织，如上图所示。

## 8. json.tool（格式化json）

```python
echo '{"foo": "bar", "baz": [1, 2, 3]}' | python -m json.tool
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144340.png)

提示：如果 json 文档无效，也会以非零状态退出。

## 9. random

我认为这可能提供一个生成随机数的实用程序，但遗憾的是它只是一个基准测试套件，没有额外的命令行选项：

```python
python -m random
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144503.png)

## 10. nntplib 

```python
python -m nntplib
```

内置演示 - 显示新闻组中的最新文章，它默认为gmane.comp.python.general：

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804144503.png)

`python -m nntplib` 这个命令的主要功能是运行 Python 解释器，并加载 `nntplib` 模块。

具体来说：

1.  `python`: 这是在命令行中运行 Python 解释器的命令。 
2.  `-m`: 这是 Python 解释器的一个选项，表示要加载一个模块进行运行。 
3.  `nntplib`: 这是要加载的模块的名称，即 `nntplib` 模块。 

当执行这个命令后，Python 解释器会加载 `nntplib` 模块，并执行其中的代码。`nntplib` 是 Python 的标准库中提供的一个模块，用于与 NNTP（Network News Transfer Protocol）服务器进行交互，实现新闻组的访问和操作。

通过运行这个命令，你可以在命令行中使用 `nntplib` 模块提供的功能，例如连接到 NNTP 服务器、获取新闻组列表、获取新闻组文章等操作。具体使用方法可以参考 Python 官方文档或 `nntplib` 模块的文档。

## 11. 显示日历（calendar）

```python
python -m calendar
```

![](https://nuibi.oss-cn-beijing.aliyuncs.com/img/20230804145054.png)
