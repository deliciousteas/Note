# pipenv教程

## 前言

1. 为什么用

起初在github上找到博主分享的代码，提示导入Requestements.txt就可以跑，没有用过于是准备了解背后的虚拟环境。

1. 是什么

pipenv将pip包管理工具和虚拟环境创建工具virtualenv结合一起，类似于npm、yarn工具。

2. 有什么用

* 包管理，projectA和B的环境彼此不会影响。
* 利于他人使用。

## 安装与使用

1. 安装

* pipenv命令行安装:pip installpipenv

* pipreqs命令行安装：为pipenv生成requirements.txt文件

2. 环境命令

* 启动环境：pipenv install
* 激活：pipenv shell
* 退出环境：exit
* 删除环境：pipenv --rm

3. 包管理

* 安装1-个包：pipenv install numpy pandas .....
* 从requirements文件安装包：pipenv install -r requirements.txt
* 删除包：pip uninstall numpy .....

4. 项目组织

生成pipfile和pipfile.locK两个文件，里面管理包之间的关系。在pycharm编辑器打开也会自动识别为pyenv环境。

![image-20240414203806512](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240414203806512.png)

5. pipenv环境依赖生成txt

pipreqs  ./ **--encoding=utf8**

> 声明utf-8很重要，详情看参考gbk报错

# 参考

[pipenv基本介绍](https://xsun4231.github.io/2019/12/12/pipenv-introduction/)

[pipenv教程](https://blog.csdn.net/qq_42951560/article/details/124224972)

[pipenv通过txt项目发布文件导包](https://ww4k.com/python/requirements_pipenv.html)

[pipenv删除环境](https://juejin.cn/s/pipenv%20%E5%88%A0%E9%99%A4%E7%8E%AF%E5%A2%83)

[reqs文件导包gbk报错](https://blog.csdn.net/weixin_45961774/article/details/109578429)