# hdfs与hbase内存管理

## hdfs与hbase关系

![HBase Working Principle: A part Hadoop Architecture | by Sahil Dhankhad |  Towards Data Science](https://miro.medium.com/v2/resize:fit:1400/1*0rsVJRwpZKfYazWaEGJSmA.png)

## 常用命令

jps：查看当前java进程

ps(process status)：查看当前系统的进程

kill：[par] [proecess-id]：强制关闭某个进程

> PID:Process ID ，进程标识符

history：查询历史命令，搭配|grep "content"查询特定命令

hbase在hdfs基础上，突破了hdfs无法对数据的随机访问。

> hadoop fs:操作任何文件系统，如本地文件系统、Amazon S3
>
> hadoop dfs：只操作dfs (古早)
>
> hdfs dfs：操作hdfs

> hdfs：Client、namenode and datanode?
>
> Client（客户端)是和hadoop文件系统通信的交互界面。具体而言，是hdfs dfs这个命令，可以跟namenode、datanode连接。

## 平衡数据节点存储不均等

start-balancer.sh

* `-threshold`: 数值越小，默认10，越小使得不同节点之间差值小到10%左右。
* -D：传递参数。如dfs.balancer.movedWinWidth(时间跨度)=300000000、dfs.datanode.balance.bandwidthPerSec（数据传输量)

##  副本管理

> 只能修改新建立的副本数

命令行：hadoop fs -setrep

hdfs-site.xml：修改副本数量，默认为3

## hbase压缩副本或者数量

> alter 'tablename', {NAME => 'columnfamily', REPLICATION_SCOPE => '1'}
>
> alter 'tablename', {NAME => 'columnfamily', COMPRESSION => 'algorithm'}有GZ、SNAPPY、LZO等等压缩算法

# 参考

[后台进程继续运行](https://help.aliyun.com/zh/ecs/support/configure-linux-to-keep-the-process-running-after-the-ssh-client-is-disconnected)

[hdfs节点之间数据平衡](https://www.cnblogs.com/qfdy123/p/14558324.html)

[修改hdfs副本数](https://blog.csdn.net/liuwei0376/article/details/91829350)

[hbase修改压缩方式](https://www.cnblogs.com/wanchen-chen/p/12934089.html)

[hadoop客户端、主节点和数据节点关系](https://github.com/wangzhiwubigdata/God-Of-BigData/blob/master/%E5%A4%A7%E6%95%B0%E6%8D%AE%E6%A1%86%E6%9E%B6%E5%AD%A6%E4%B9%A0/Hadoop-HDFS.md)

[what is client in hadoop](https://stackoverflow.com/questions/43221993/what-does-client-exactly-mean-for-hadoop-hdfs#:~:text=The%20basic%20filesystem%20client%20hdfs,to%20read%2Fwrite%20block%20data.)

[hbase简介](https://github.com/wangzhiwubigdata/God-Of-BigData/blob/master/%E5%A4%A7%E6%95%B0%E6%8D%AE%E6%A1%86%E6%9E%B6%E5%AD%A6%E4%B9%A0/Hbase%E7%AE%80%E4%BB%8B.md)

[hadoop快速入门介绍](https://github.com/wangzhiwubigdata/God-Of-BigData/blob/master/Hadoop/Hadoop%E6%9E%81%E7%AE%80%E5%85%A5%E9%97%A8.md)