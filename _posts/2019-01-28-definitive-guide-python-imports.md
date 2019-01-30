---
layout: post
title: The Definitive Guide to Python import Statements
categories: [Python]
description: The Definitive Guide to Python import Statements
keywords: Python import
---

Python 的 import 怎么用？一文详解

---
> 本文译自：[链接](https://chrisyeh96.github.io/2017/08/08/definitive-guide-python-imports.html)

# 总结/关键点

- `import` 声明会搜索 `sys.path` 的路径列表
- `sys.path` 总是包含从命令行运行的脚本所在的路径，但并非包含命令行的当前工作目录
- 导入一个包（packet）相当于导入包的 `__init__.py` 文件

# 基本定义
- 模块（module）：任何 `*.py` 文件。模块名就是文件名。
- 内置模块（built-in module）：被编译到 Python 解释器的（用 C 写的）模块，因此没有 `*.py` 文件。
- 包（packet）：任何包含名字是 `__init__.py` 文件的文件夹。包的名字就是文件夹的名字。
	* 在 Python3.3 及以上，任何文件夹（即使没有 `__init__.py` 文件）也会被认为是一个包。
- 对象（object）：在 Python 里，几乎所有都是对象——函数，类，变量，等等。

# 目录结构例子
```
test/                      # root folder
    packA/                 # package packA
        subA/              # subpackage subA
            __init__.py
            sa1.py
            sa2.py
        __init__.py
        a1.py
        a2.py
    packB/                 # package packB (implicit namespace package)
        b1.py
        b2.py
    math.py
    random.py
    other.py
    start.py
```
注意我们没有在 `test/` 文件夹里面放置 `__init__.py` 文件。

# 什么是 `import`？

- 当一个模块被 import 之后，Python 运行所有的模块文件里的代码。
- 当一个包被 improt 之后，Python 运行包中  `__init__.py` 文件（如果存在）中的所有代码。
import之后，所有模块以及包的 `__init__.py` 文件中定义的对象就都可用了。

# `import` 和 `sys.path` 基础

根据Python文档，下面是import声明如何搜索正确的模块或者包来import：

> 当import一个称为spam的模块的时候，解释器首先在内置模块中搜索同名模块。如果没有找到，它会在变量sys.path给定的目录列表中搜索名为spam.py的文件。sys.path会从以下位置初始化：
>
> - 包含输入脚本的目录（若无文件指定则为当前目录）
> - PYTHONPATH（目录名的一个列表，使用与shell变量PATH相同的语法）
> - 依赖于安装的默认值
>
> 初始化之后，Python程序可以修改sys.path。正在运行的脚本所在的目录被放在搜索路径的开头，在标准库路径之前。这意味着那个目录中的脚本将会优先于相同名称的库被载入。来源：Python2和3

技术上来讲，Python文档是不完全的。解释器不仅会寻找名为spam.py的文件（也即模块），也会寻找名为spam的文件夹（也即包）。

注意Python解释器首先在内置模块（即被直接编译进Python解释器里的模块）里寻找。内置模块的列表是和安装相关的，并且可以在sys.builtin_module_names找到（Python2 和 Python3）。其中一些常见的内置模块包括sys（总是包括），math，itertools，和time等。

不像内置模块会被在搜索路径中首先搜索，Python标准库中的其他模块排在当前脚本所在目录之后。这将导致一个令人困惑的行为：有可能代替但是并非全部的Python标准库。例如，在我的电脑上（Windows10， Python3.6），math模块是内置模块，但是random就不是。因此，在start.py中的import math将会从Python标准库中导入math模块，而不是我自己的math.py。然而，start.py 中的 import random将会导入我自己的random.py文件，而不是从Python标准库导入。

另外，Python的import是大小写敏感的。import Spam与import spam是不同的。

函数pkgutil.iter_modules（Python2 和 Python3）可以被用于得到从一个给定路径下，所有可导入的模块的列表（不包含Python标准库）：

```python
import pkgutil
search_path = '.' # set to None to see all modules importable from sys.path
all_modules = [x[1] for x in pkgutil.iter_modules(path=search_path)]
print(all_modules)
```

资源

- [How to get a list of built-in modules in python?](https://stackoverflow.com/q/8370206)
- 感谢 [etene](https://github.com/etene) 指出Python标准库中内置模块和其他模块的区别。

## 关于sys.path的更多

为了查看sys.path示什么，在解释器里运行以下代码或者作为脚本运行：

```python
import sys
print(sys.path)
```

Python对于sys.path的文档是这么描述的...


> 一个指定了模块搜索路径的字符串列表。从环境变量PYTHONPATH初始化，加上依赖于安装的默认值。
>
> 在程序启动初始化的时候，此列表的第一项path[0]是调用Python解释器的脚本所在的目录。如果脚本目录不可用（例如，如果以交互方式调用解释器或者从标准输入读取脚本），path[0]就是空字符串，它指示Python首先搜索当前目录中的模块。注意脚本目录是插入在PYTHONPATH结果之前的。
>
> *来源：Python 2 和  3*

Python的命令行界面文档添加了有关从命令行运行脚本的以下内容。具体而言，当运行python <script>.py，然后...

> 如果脚本名直接引用Python文件，那么包含该文件的目录就被加入到了sys.path的开头，然后文件作为主模块执行。
>
> *来源：Python 2 和  3*

让我们回顾一下Python搜索要导入的模块的顺序：

1. 在Python标准库中的模块（如math，os）

2. 由sys.path指定的目录中的模块或者包：

   1. 如果Python解释器是交互式运行的：

      - sys.path[0]是空字符''。这告诉Python搜索启动解释器的当前工作目录，即Unix系统上的pwd输出

      如果通过python <script>.py 运行脚本：

      - sys.path[0]是 <script>.py的路径

   2. 在PYTHONPATH环境变量里的目录

   3. 默认的sys.path位置

注意当运行一个Python脚本的时候，sys.path并不关心你当前的工作目录是什么。它只关心脚本的路径。例如，如果我的shell在test/文件夹，并且我运行python ./packA/subA/subA1.py，然后sys.path就包含了 test/packA/subA/ 而非 test/。

另外，sys.path在所有的导入的模块中共享。例如，假设我们调用python start.py。让start.py导入packA.a1，并且让a1.py打印sys.path。然后sys.path会包含test/（start.py的路径），而不是test/packA（a1.py的路径）。这意味着a1.py可以调用import other 因为other.py是test/文件夹下的一个文件。

# 关于`__init.py__`的所有

一个`__init.py__`文件有两个功能：

1. 将文件夹中的脚本转化为可导入的包中的模块（Python 3.3 之前）

2. 运行包初始化代码

## 将文件夹中的脚本转化为可导入的包中的模块

