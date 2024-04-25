

## 进程管理

ctrl+c中止命令，ctrl+z会暂停命令

&符号 添加在命令后面，是将命令放在后台。

jobs：查看进程运行情况。

* jobs -r 显示正在运行得后台作业

kill：kill进程

* kill %1
* kill PID

nohup：no hang up会在系统后运行命令，退出终端也不影响。默认情况下会在当前目录下输出一个nohup.out文件。

## 文件系统层次结构

/bin:程序文件

* /lib文件：依赖库文件，bin可以直接运行

/boot：启动系统时需要的文件

/dev：存储设备文件

/opt:额外的程序包，一般应用程序放置于此

* 可以理解为linux在opt目录安装在分发包范围之外的包。
* /usr/local：安装分包管理器下载的包就行。

> 通常情况下，安装软件应该优先考虑使用包管理器来进行.

## 标准输入与输出

stdin、stdout、stderr，其中std是standard缩写，在linux中编号分别是0、1、2。默认为你的终端。

"<"是重定向输入，一个则是覆盖原有内容，两个"<<"是追加。

">"是重定向输出

# 网络、文本处理工具

wget、curl(擅长网络请求）、aria2、mwget、axel....

wc命令：输出行数、单词书、字节数

head(tail)命令：

* -n 指定行数
* -c 指定字节数

# 参考

[linux jobs命令](https://bashcommandnotfound.cn/article/linux-jobs-command)

[nohup命令](https://www.runoob.com/linux/linux-comm-nohup.html)

[opt和usr区别](https://askubuntu.com/questions/34880/use-of-opt-and-usr-local-directories-in-the-context-of-a-pc)

[重定向输入与输出](https://101.lug.ustc.edu.cn/Ch06/#redirection)

[Linux上的编译](https://101.lug.ustc.edu.cn/Ch07/#py-implementations)