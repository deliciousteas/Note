**jps参数**

Namenode：hadoop主服务器

secondaryNamenode：冗余

NodeManager：yarn中namenode节点的代理

**ResouceManager**：yarn中管理资源调配ResouceManager

Hmaster：管理habse的

QuorumPeerMain：zookeeper

Worker：yarn中表示**NodeManage**r所在节点

# Hbase数据格式

特点：一次写入，多次读取，以字节来管理。

修改数据：

* 情况：hbase基于hdfs存储，而hdfs文件写入后无法修改
* 时间戳：不删除，通过时间戳指向新的数据即可，但旧数据没有删除。

查找数据：

* 四维坐标定位：Row行、Column Family列簇、Column Qualifier列标识、Timestamp时间戳
* Cell 单元：有行、列簇、列标识共同组成的一个单元，存储在单元内的数据成为cell。

### hbase代码

Admin：Hbase管理员权限的API。

hbase shell中删除某个table：

* disable "   xxx"

* drop  "tablename"

# 问题

![image-20240413135648625](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240413135648625.png)

hbase中出现unhealth datanode，spark命令开启的任务会一直accpting，而不会running。

# 解答

### 1. Linux命令

hbase是基于内存，如果内存空间不足将不会再进行，所以上述代码运行四个会消失还未结束。

> stop-yarn.sh不起作用原因，直接用kill干掉。(kill 可以强制java相关进程)
>
> 然后重启一般是stop-all.sh，再重新启动hbase、spark、hadoop即可完成重启。

**相关命令**

* history命令：可以查看以前的命令，一个月内命令足够看了。

* firefox：开源软件，linux联系紧密。所以基本linux都支持在命令行输入firefox打开浏览器。

* jps：加载正在运行的java进程信息。PID是进程号，唯一标识。

* kill命令：kill进程，kill -9杀死一个进程。所以kill命令和jps配合。

**配置参数修改**

修改配置后，需要重启，stop-all.sh，停止不了再用kill+jps强制停止。然后start-all.sh重启，顺序为hadoop、spark、hbase，需要进入各自目录用*.sh重新启动。

spark中master管理集群和系统但不参与计算，worker计算节点。

debug用于本地测试调试代码，jar包在集群运行考虑看log日志输出

### 2. 查看sprak命令报错

jar包保存后，原本应该在控制台输出内容，在yarn的webui里面worker节点上可以具体点进去为serr和sout文件。

* sout：控制台数据输出内容
* serr：代码相关报错。

> 实验室电脑可以ssh云服务器主节点，但是我无法访问其他四个内网节点的log日志，所以得通过VNC登录主节点才能看到运行报错日志。🤣🤣🤣🤣🤣🤣

### 3. hbase数据存储方案

通过hbase上传得知哪个文件有问题，hdfs也不能改，只能在本地修改数据。且上传每行数据默认10MB，如果要提高需要造hbase-site.xml中添加参数设置20....

###  4. encode and decode

**encode: change sth secretly,编码**

**decode：discover the meaning of info in a secret解码**



# 参考

https://blog.csdn.net/weixin_38653290/article/details/108218078

[Stop-yarn.sh作用](https://developer.aliyun.com/ask/365351)

[jps各个参数](https://blog.csdn.net/zxl646801924/article/details/84788707#:~:text=1.Namenode,%E7%9A%84%E5%85%83%E6%95%B0%E6%8D%AE(metadata)%E3%80%82)

[启动时HADOOP_路径被替换](https://blog.csdn.net/weixin_41485724/article/details/105254009)

[hbase数据格式：视频](https://www.bilibili.com/video/BV1kJ411J77b/?spm_id_from=333.337.search-card.all.click&vd_source=b61ce8d81a5e8e82447077f84ae7352a)

[habse数据基本概念](https://andr-robot.github.io/HBase%E5%9F%BA%E7%A1%80%E6%9E%B6%E6%9E%84/)

[修改输出重定向](http://lxw1234.com/archives/2015/05/205.htm)

[python：爹系语言](https://www.cnblogs.com/wenBlog/p/8441231.html)