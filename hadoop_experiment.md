本次实验所用hadoop version是3.13  
# hadoop版本介绍：
1.0已淘汰，HDFS+MAPREDUCE
2.0 HDFS+YARN+MAPREDUCE
3.0 更加稳定 
# hadoop文件夹目录介绍 
etc：hadoop配置文件所在目录  
bin：hadoop管理脚本和使用脚本的目录，是sbin目录下的基础实现。  
sbin：hadoop中包含HDFS和YARN各类服务启动的事情。
share：hadoop各模块编译后的jar所在目录。
include：用于c++访问HDFS或者写mapreduce程序。
# hadoop配置文件说明  
1. **core-site.xml**  
fs.defaultFS :file://  
hadoop.tmp.dir: /tmp/hadoop-${user.name}
2. **hadoop-env.sh**  
HDFS_NAMENODE_USER、HDFS_DATANODE_USER、HDFS_SECONDARYNAMENODE_USER启动用户限制  
3. **hdfs-site.xml**  
dfs.namenode.secondary.http-address 是http通过的端口  
dfs.replication 副本个数  
dfs.namenode.name.dir:namenode's log location  
dfs.datanode.data.dir:datanode's log location   
4. **mapred-site.xml**  
mapreduce.framework.name: yarn stands for MR version 
mapreduce.jobhistory.address:jobhistory's output address   
mapreduce.jobhistory.webapp.address:webAPP's port  
yarn.app.mapreduce.am.env: yarn wokringSpace  
mapreduce.map.env: map workSpace  
mapreduce.reduce.env: reduce workSpace  
5. **Yarn-site.xml**  
yarn.resourcemanager.hostname: responsible for tracking the resources in a cluster, and scheduling applications.  
ps:> DFS: distributed FileSytem


# hadoop支持语言
官方推荐java，python、c++也可。  
mapreduce模块中python可以用hadoop Stream，c++可以用hadoop Pipes  
> 什么是jar包？ 
Java ARchive,文件后缀名：*.jar   
通常聚合大量的java类文件、相关元数据和资源到一个文件，便于分发java平台软件和库。
# 参考内容：
[hadoop各版本和文档目录介绍](https://zhuanlan.zhihu.com/p/568671274)  
[hadoop入门教程](https://hustlijian.github.io/tutorial/2015/06/19/Hadoop%E5%85%A5%E9%97%A8%E4%BD%BF%E7%94%A8.html)  
----
# 遇到的问题
## 1. 集群启动permission denied  
> 描述：之前五台机器都是hdfs用户，但操作后误删了hdfs用户的home目录，于是想用hadoop用户来启动hadoop代码，结果出现了SSH问题和hadoop启动问题。执行hadoop的start-dfs.sh命令启动不了，集群中五个节点都提示permission denied。五台节点分别是boss，woker1、2、3、4，其中用户分别是hadoop、hdfsx4。
### SSH问题
1. hadoop用户与其他hdfs用户所在的集群没有建立ssh密钥。
2. authorized_keys、./.ssh、id_rsa文件（夹）权限。
- 集群用户名问题
1. 集群内部的五台节点，应该是相同的用户名。
2. 查找用户名，发现namenode存在hdfs用户的mail，但是home目录已经误删，于是删除、重新生成用户并添加home目录，设置文件所有者等等。
3. hadoop-env.sh设置启动用户名字
### 解决步骤：
1. 重新配置SSH密钥对：重新为hadoop用户生成key，然后整理authorized_keys，将公钥五台机器同步，并修改五台机器相关SSH的文件(夹)权限。
2. 恢复HDFS用户的Home目录和Hadoop相关目录的权限：SSH问题解决后，彼此SSH切换丝滑，但是只要使用start-dfs.sh命令就提示permission denied，重新搜索问题，发现hadoop用户+hdfs用户*4的集群启动不了，看到有帖子说hdfs启动不了是因为集群节点登录用户name不一样，即其他节点无法识别该namenode的username。所以将namenode所在节点添加用户hdfs，重新设置SSH配置和hadoop-env.sh中的HDFS_NAMENODE_USER等登录变量。
### 问题总结：
界定问题花费了大量时间，主要测试SSH问题和集群节点用户名字。
### 收获：
1. 查看hadoop目录下的log日志，并为命令启动失败查看错误日志。通过查看日志指导datanode根本没有启动起来，问题卡在SSH连接上的问题。
2. ssh有参数-v可以准确查看命令运行过程。
3. ⚠️（ssh问题一般不用修改这）能够限制SSH以普通用户登录或者root用户登录：/etc/ssh/sshd_config
4. gpt帮助有限。  
## hadoop启动jps没反应  
1. **namenode的log日志有WARN**  
描述：  
2023-12-20 16:55:57,079 **WARN** org.apache.hadoop.hdfs.server.namenode.FSNamesystem: Only one image storage directory (dfs.namenode.name.dir) configured. Beware of data loss due to lack of redundant storage directories!  
2023-12-20 16:55:57,080 **WARN** org.apache.hadoop.hdfs.server.namenode.FSNamesystem: Only one namespace edits storage directory (dfs.namenode.edits.dir) configured. Beware of data loss due to lack of redundant storage directories!   
解决方案：   
创建保存文件路径，然后在hdfs-site.xml文件中修改namenode备份位置。  
rm命令删除./tmp文件夹，然后重新./bin/hdfs namenode -format  

2. **JPS不显示namenode**  
用jps没有任何进程加载，咨询师兄后用的ps进程查看。  
jps is Experimental and Unsupported tool,用ps命令替代.    
![d34b78db4cc542ce3d5d0291c03d301](https://github.com/deliciousteas/Note/assets/107855849/7739ba9c-d6a9-41b1-9b1d-5339c90efc51)

> ps命令：
`ps -ef |grep hadoop(NameNode)`   
### 参考：
[ssh密钥必须是700](https://www.jianshu.com/p/7de5a612799e)  
[ssh密钥权限](https://blog.51cto.com/merrycheng/1340280)  
[hadoop启动jps不显示](https://blog.csdn.net/NIE_WIN/article/details/120741695)  
[删除用户命令](https://askubuntu.com/questions/459365/how-to-delete-a-user-its-home-folder-safely)  
[启动hdfs失败的几种情况](https://www.cnblogs.com/suhaha/p/9440557.html)  
[jps命令](https://www.cnblogs.com/heihaozi/p/16007667.html#:~:text=jps%EF%BC%88Java%20Virtual%20Machine%20Process,%E5%94%AF%E4%B8%80ID%EF%BC%88LVMID%EF%BC%8CLocal%20Virtual)  
[ps命令](https://www.runoob.com/linux/linux-comm-ps.html)  
