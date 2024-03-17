# opencascade环境配置教程|总结

> 背景：研究生在读，近期开始学习opencascade源码和使用，业务上需要利用它来几何计算，使用逻辑是先建模再计算。这篇内容将从如何获取源代码、编译，windows环境下的编译、链接常见问题分析、梳理opencascade类的继承关系三个内容部分展开。  
希望通过这一系列介绍能够帮助大家快速上手opencascade环境配置以及研究使用，同时记录自己学习过程。如果有什么问题欢迎联系。

 # 什么是opencascade
opencascade是c++语言编写的几何计算库，开源使用，提供python和c++两种使用版本，支持可视化、建模、计算，输入输出文件为.BRep文件。同样CGAL也是c++的几何计算库应用于各行各业，Opencascade因广泛应用于CAD产业而出名，笔者由于不是这一领域所以无法对两者库做出对比。🤣🤣
 # opencascade_继承关系
opencascade有非常多的头文件，总结前缀开头其实主要有GP、Geom、TopoDS开头等等为主，并且彼此之间具有继承关系，下面是我对这些类的初步梳理：
GP_xxx：基本单位如point、vector...  
Geom_xxx：几何构型  
TopoDS_XXX:复杂几何构型  
其中GP->Geom,是通过GC_xxx方法实现；Geom_xxx-> TopoDS_xx是通过BRepBuilderAPI发放实现，TopoDS_xxx ->Brep（这一步还没实现我也不大确定）是通过BRepPrimAPI_xxx方法实现。  
opencascade中的shape是TopoShape类型，在它的子类中还有vertex、Edge、Wire、mesh、Solid等类型。
 # 下载源代码
opencascade是开源的代码，可以从官网下载，建议下载源码版本，然后下载第三方库，记得下载x64位，具体操作可以查看参考链接。
 # vs环境配置
这一部分主要解释环境配置易出现的问题以及问题背后的解释，帮助大家认识问题来源，尤其hh，笔者之前不会写代码😒
## 1. 编译和链接  
在VisualStudio中，一个cpp程序的运行需要经过两部分处理，编译+链接。
编译是将源码（c++代码）转换成目标代码，也就是obj文件，不可直接执行。而且编译还会生成其他中间文件，如预编译投文件。
链接是在程序运行时，将多个对象文件（obj）与库文件（如lib库）链接生成最终可执行文件（.exe）。
## 2. lib、dll、pdb 文件关系
lib文件，是静态库文件，包含目标代码，在链接时被直接并入可执行文件，其中包含对其他库文件的引用信息，以供链接时解析。
dll文件，动态链接库文件，包含头文件中声明的函数和变量的实现。
lib和dll文件中都包含obj文件，但不包含c/c++头文件的源代码，头文件会在编译前全部展开到源代码中。
pdb文件：debug时需要，显示源代码辅助。
## 3. 编译错误和链接错误  
在VS中，编译错误主要出现在(compile)阶段，表现位代码语法、引用头文件的错误，源代码会显示红色波浪线。典型的为语法错误、拼写错误、缺少头文件等。
链接错误：(Link)阶段与依赖库设置有关。这类错误一般是缺少库文件、库文件版本不匹配、函数未定义等等。需要检查附加依赖库路径、配置-调试-工作环境。
 ### 3.1 vs环境配置-链接错误
opencascade链接配置有三步步骤，首先你得要配置依赖库路径，然后添加准确的lib库文件名，再是在项目属性-调试器-工作环境中添加dll文件、pdb文件路径，以*PATH="dll、pdb文件路径" %PATH%*格式添加。
    
其中最麻烦的部分是程序运行报错，显示为LINK错误时，是一堆16进制的函数名称，显示为未识别的符号，如@xxxadaweaweaweaw4579的字符。这里我们可以使用*Far Manager*工具，在工具打开的命令行中，切换到lib库所在路径，然后copy十六进制的函数，程序会遍历查找，然后手动在vs环境中输入库名字即可。

> Far Manager：俄罗斯人创始，是一个在Windows上运行的文件管理器和文本编辑器，提供俄罗斯语和英文。 
   
___
 
## 参考链接   
### FarManager
[Far Manager下载地址](https://www.farmanager.com/)  
[Far Manager使用语法](https://blog.csdn.net/huluwaaaa/article/details/101833993#:~:text=Ctrl%20%2B%20%26%5D%EF%BC%9A%E5%89%8D%E5%BE%80%E6%A0%B9%E7%9B%AE%E5%BD%95%E3%80%82%20Ctrl%20%2B%20U%EF%BC%9A%E4%BA%A4%E6%8D%A2%E5%B7%A6%E5%8F%B3%E9%9D%A2%E6%9D%BF%E3%80%82,Alt%20%2B%20F1%EF%BC%9A%E5%88%87%E6%8D%A2%E5%B7%A6%E9%9D%A2%E6%9D%BF%E7%9A%84%E7%9B%98%E7%AC%A6%E3%80%82%20Alt%20%2B%20F2%EF%BC%9A%E5%88%87%E6%8D%A2%E5%8F%B3%E9%9D%A2%E6%9D%BF%E7%9A%84%E7%9B%98%E7%AC%A6%E3%80%82)  
### VisualStudio配置教程
[VS配置opencascade_GIF教程](
https://zhuanlan.zhihu.com/p/538399108)  
[vsDebug模式配置dll库路径](https://blog.51cto.com/u_15088375/3247722)  
### Opencascade层次关系
[opencascade类层次关系](https://blog.csdn.net/u012541187/article/details/81021064)
