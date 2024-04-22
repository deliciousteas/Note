# python

library是直接来import完成功能的，十分方便。package是对module的组合，any *.py可以视为一个module。

module：*.py结尾，组成由变量和方法组成，可以对他再次创建修改。

Build-in module：内置模块，如math、os、datatime、random。

package是一系列module的合计

library是编译好的库。如numpy、networkx，matplotlib

## module和package区别

module通常以.py作为文件扩展名，可以在其他程序中导入和是用。

package是一种模块的组织，包含一个__init__.py文件表示他是一个包。

模块是一个单独的Python文件，而包是一个包含多个模块和子包的目录结构。包可以帮助更好地组织和管理代码，使得代码结构更清晰、更易于维护

## module和library区别

模块是一个单独的Python文件，而库是一组相关的模块或功能集合

## library和pacakge的区别

包是一种用于组织和管理模块的方式，通常是一个包含__init__.py文件的目录

库是一组相关的功能或模块的集合，用于解决特定领域或问题。

todo：如何构建一个package 并打包呢？

## __init__函数作用

存储package‘s内容，一个空的init.py使得所有function都被import，当然optional 自定义import哪些函数是允许的。

`

from module1 import *
from .module2 import *

if condition:
    from .module1 import specific_function1
    from .module2 import specific_function2

`

# python 打包？

将python文件的依赖项、程序、配置文件、数据文件一起打包成一个单独的可执行文件或者安装包，以便其他人使用。

参考：

> [module in python](https://www.tutorialsteacher.com/python/python-package)
>
> [python packageing](https://blog.csdn.net/m0_74587019/article/details/134101649)