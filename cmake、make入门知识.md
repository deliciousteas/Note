# cmake vs make
> 该篇博客记录了楼主自学cmake和make过程，适合受众为项目构建小白，介绍了linux项目构建概念和实验总结，分享cmake和make教学链接。

## 什么是make
make是linux下的命令
如果目录下有Makefile文件，那么make命令可以生成项目。  
步骤：Makefile文件👉make命令👉项目

### make实验
> 实验参考内容见底部 

MakeFile文件的语法格式:   
`target:dependenncies`  
`<tab> command`  
翻译过来就是第一行 ：目标文件：依赖文件    
第二行：tab键空开距离，command写命令，案例中是用g++命令生成中间文件、链接。生成target项目（target也是它的名字）  
然后再·make·命令生成该二进制文件。  
## 什么是cmake
cmake是跨平台的项目构建工具，可以再win、linux上用。   
cmake的构建步骤：
CMakeLists.txt 👉cmake👉Makefile文件👉Make命令👉项目
### cmake实验
> 实验参考内容见底部

步骤上比make多一步：  
1. CMakeLists.txt文件  
`cmake_minimum_required`  `add_executable`  `target_include_directories`  `project`都是命令，相应的设置cmake需要的最小版本，将source源码添加到什么二进制执行文件， include依赖目录，project设置项目名称。  
部分命令会生成变量，如下方代码中的project命令会生成变量PROJECT_NAME,可以在add_executable中替换第一个参数：
```# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
cmake_minimum_required(VERSION 3.5)

# Set the project name
project (hello_headers)

# Create a sources variable with a link to all cpp files to compile
set(SOURCES
    src/Hello.cpp
    src/main.cpp
)

# Add an executable with the above sources
add_executable(hello_headers ${SOURCES})

# Set the directories that should be included in the build command for this target
# when running g++ these will be included as -I/directory/path/
target_include_directories(hello_headers
    PRIVATE 
        ${PROJECT_SOURCE_DIR}/include
)
```
2. Makefile  
```
$make
$./你的project-NAME
```


##  make和cmake使用区别
make和cmake都需要写文档，只不过make是写makefile文件，cmake是写cmakelist文件，两者语法、写法不同，了解怎么构建简单项目即可。  


![cmake和make之间工作关系](https://img-blog.csdnimg.cn/img_convert/c88be0810d0233462db9f985f1e0b2c5.png)

# 参考内容  
[cmake和make区别：windows、linux版](https://earthly.dev/blog/cmake-vs-make-diff/#:~:text=In%20summary%3A%20The%20difference%20between,used%20to%20create%20a%20Makefile.)  
[cmake教程](https://github.com/ttroy50/cmake-examples/tree/master/01-basic)  
[cmake中文教程](https://github.com/SFUMECJF/cmake-examples-Chinese/tree/main/01-basic)  
[make教程](https://earthly.dev/blog/cmake-vs-make-diff/#top)  
ps：`make教程`中文件名有错误，没有hello.cpp，自行改为main.cpp即可
