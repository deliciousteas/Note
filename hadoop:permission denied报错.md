# 描述：  
> 之前五台机器都是hdfs用户，但操作后误删了hdfs用户的home目录，于是想用hadoop用户来启动hadoop代码，结果出现了SSH问题和hadoop启动问题。
> 执行hadoop的start-dfs.sh命令启动不了，集群中五个节点都提示permission denied。五台节点分别是boss，woker1、2、3、4，其中用户分别是hadoop、hdfsx4。
- # SSH问题
1. hadoop用户与其他hdfs用户所在的集群没有建立ssh密钥。
2. authorized_keys、./.ssh、id_rsa文件（夹）权限。
- # 集群用户名问题
1. 集群内部的五台节点，应该是相同的用户名。
2. 查找用户名，发现namenode存在hdfs用户的mail，但是home目录已经误删，于是删除、重新生成用户并添加home目录，设置文件所有者等等。
3. hadoop-env.sh设置启动用户名字
# 解决步骤
1. **重新配置SSH密钥对**：重新为hadoop用户生成key，然后整理authorized_keys，将公钥五台机器同步，并修改五台机器相关SSH的文件(夹)权限。
2. **恢复HDFS用户的Home目录和Hadoop相关目录的权限**：SSH问题解决后，彼此SSH切换丝滑，但是只要使用start-dfs.sh命令就提示permission denied，重新搜索问题，发现hadoop用户+hdfs用户*4的集群启动不了，看到有帖子说hdfs启动不了是因为集群节点登录用户name不一样，即其他节点无法识别该namenode的username。所以将namenode所在节点添加用户hdfs，重新设置SSH配置和hadoop-env.sh中的HDFS_NAMENODE_USER等登录变量。
# 问题总结
界定问题花费了大量时间，主要测试SSH问题和集群节点用户名字。
# 收获
1. 查看hadoop目录下的log日志，并为命令启动失败查看错误日志。通过查看日志指导datanode根本没有启动起来，问题卡在SSH连接上的问题。
2. ssh有参数-v可以准确查看命令运行过程。
3. ⚠️（ssh问题一般不用修改这）能够限制SSH以普通用户登录或者root用户登录：/etc/ssh/sshd_config
4. gpt帮助有限。
# 参考：
[ssh密钥必须是700](https://www.jianshu.com/p/7de5a612799e)  
[ssh密钥权限](https://blog.51cto.com/merrycheng/1340280)  
[hadoop启动jps不显示](https://blog.csdn.net/NIE_WIN/article/details/120741695)  
[删除用户命令](https://askubuntu.com/questions/459365/how-to-delete-a-user-its-home-folder-safely)  
[启动hdfs失败的几种情况](https://www.cnblogs.com/suhaha/p/9440557.html)  
