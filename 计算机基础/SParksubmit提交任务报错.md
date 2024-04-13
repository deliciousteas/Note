# 分布式环境配置

首先配置java环境，idea的linux-version

然后配置Hadoop环境及其组件，然后安装Hdfs、Yarn组件，ZooKeeper、hbase、Sparj。

1. **HDFS**：首先安装和配置 HDFS，因为它是整个 Hadoop 生态系统的基础存储组件。
2. **YARN**：安装和配置 YARN，以便在集群中管理和分配资源给其他计算框架。
3. **ZooKeeper**：安装和配置 ZooKeeper，作为 HBase 和其他分布式系统的协调服务。
4. **HBase**：最后安装和配置 HBase，以便在 Hadoop 集群上运行分布式的面向列的数据库。
5. **Spark**：最后安装和配置 Spark，可以选择将其与 YARN 集成以共享集群资源。

# hbase-KeyValue过大

问题：`hbase.server.keyvalue.maxsize`默认为10MB(属性需转为字节流),文件有若干行>=10MB写不进去

方法：

1. hbase-site.xml文件中添加配置

<property>

<name>hbase.server.keyvalue.maxsize</name>

<value>31457280</value>

</property>

2. java代码中显式配置KeyValue值为＞10MB

# Yarn：Web报错

yarn是一个资源管理组件，在WebUI界面中会显式你所有的application及其相关信息。

其中AM是ApplicationMaster，管理该任务的整个运作过程，ResourceManager(RM)负责全局任务，worker是工作节点。

* **memory total**:yarn集群管理的内存总和。

![](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240411104311944.png)

* VCores Total：yarn集群管理cpu-core的数量，实际上没用起来，只用了一块cpu

![image-20240411104532942](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240411104532942.png)

最大分配为8G，4核心

* ![image-20240411112047092](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240411112047092.png)

如下图所示进入某个Application的界面，会发现界面最后状态是FAILED，报错原因在下，如果需要查看确切错误需要划到最下方看该application的subTask在哪个集群节点运行并查看它的log日志。

![image-20240413090140869](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240413090140869.png)

# SPark-submit命令

Spak任务提交后，一直处于Accept状态，无法正常运行，直到显示Timed Out.

将原本的命令从`spark-submit --master yarn --deploy-mode cluster --class BIMSearch.APP --jars /data/workspace/xxxxx/target/xxxxxxx.jar --num-executors 10 --executor-cores 2 --executor-memory 4G --driver-core 8 --driver-memory 16G --name test  hdfs://boss:xxxx/xxxx/Whole_data_003.txt`修改为`spark-submit --class org.example.App --master yarn --deploy-mode cluster --executor-memory 3G     --executor-cores 1 --num-executors 32  --conf spark.default.parallelism=32  --conf spark.network.timeout=10000 --conf spark.executor.heartbeatInterval=10000 /data/workspace/xxxxx/target/xxxxxxxxxx.jar`

其中driver是负责任务和结果分发，executor 负责数据处理任务执行。

1. **--num-executors**：这个参数指定了应用程序运行时的 Executor 进程数量，即在集群中启动的 Executor 的个数。每个 Executor 负责执行应用程序中的任务，并管理分配给它的内存和 CPU 资源。在这个例子中，`--num-executors 10` 表示会启动 10 个 Executor 进程。
2. **--executor-cores**：这个参数指定了每个 Executor 进程的 CPU 核心数。Executor 是在集群中的工作进程，用于执行应用程序中的任务。`--executor-cores 2` 表示每个 Executor 进程会被分配 2 个 CPU 核心来执行任务。
3. **--executor-memory**：这个参数指定了每个 Executor 进程可以使用的内存大小。它表示每个 Executor 进程分配的内存量。在这个例子中，`--executor-memory 8G` 表示每个 Executor 进程被分配了 8GB 的内存。
4. **--driver-cores**：这个参数指定了 Driver 进程的 CPU 核心数。Driver 是 Spark 应用程序的控制节点，负责整个应用程序的执行和管理。在这个例子中，`--driver-cores 16` 表示 Driver 进程会被分配 16 个 CPU 核心。
5. **--driver-memory**：这个参数指定了 Driver 进程可以使用的内存大小。它表示 Driver 进程分配的内存量。在这个例子中，`--driver-memory 16G` 表示 Driver 进程被分配了 16GB 的内存。

# 参考

[hbase命令行教程](https://www.cnblogs.com/ityouknow/p/7344001.html)

[hbase基础介绍](https://www.cnblogs.com/lori/p/13554859.html)

[spark-submit提高传输效率参数](https://cloud.tencent.com/developer/article/1739473)

[yarn webui参数](https://blog.csdn.net/weixin_42411818/article/details/96283995)

[yarn运行超时，改变内存test？](https://stackoverflow.com/questions/40740750/timeout-exception-in-apache-spark-during-program-execution)

[spark-submit实际生产参数](https://blog.csdn.net/qq_33689414/article/details/80621578)

[yarn-site.xml文件修改容器内存](https://www.cnblogs.com/wenBlog/p/12220897.html)

[查看habse状态](https://www.cnblogs.com/caoweixiong/p/11268919.html)

[hdfs节点unhealthy](https://blog.51cto.com/u_13707997/5066212)

[hdfs端口类型](https://blog.csdn.net/weixin_43135178/article/details/107331353)

[hdfs文件访问](https://www.cnblogs.com/shoufeng/p/14879045.html#31--%E8%8E%B7%E5%8F%96%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E9%87%8D%E8%A6%81)

[hdfs上访问文件参考：csdn](https://blog.csdn.net/shuyv/article/details/110391099)

[hbase端口](https://www.google.com/search?q=hbase%E4%B8%AD+2181%E6%98%AF%E4%BB%80%E4%B9%88%E7%AB%AF%E5%8F%A3&oq=hbase%E4%B8%AD+2181%E6%98%AF%E4%BB%80%E4%B9%88%E7%AB%AF%E5%8F%A3&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIHCAEQIRigATIHCAIQIRigATIHCAMQIRigAdIBCDczMDNqMGo0qAIAsAIB&sourceid=chrome&ie=UTF-8)

[driver和executor区别与关系](https://www.cnblogs.com/-courage/p/15338881.html)

[spark-submit一直accepted而不uploaded](https://blog.csdn.net/qq_26222859/article/details/48788473)