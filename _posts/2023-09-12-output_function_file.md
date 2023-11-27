---
title: '输出函数所在文件'
date: 2023-09-12
permalink: /posts/2023/09/output_function_file/
tags:
  - Code Repository
---

- 输出函数所在文件，避免找不到函数所在文件夹或者文件

``` python
# -*- coding:UTF-8 -*-
import inspect

def my_function():
    pass

# 获取函数的文件路径
function_file = inspect.getsourcefile(my_function)

print(f"The function '{my_function.__name__}' is defined in the file: {function_file}")

# 输出类所在文件
import sys
import os
print(os.path.abspath(sys.modules[create_model.__module__].__file__))
```