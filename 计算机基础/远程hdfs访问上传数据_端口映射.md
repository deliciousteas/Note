## 远程hdfs访问上传数据：端口映射

环境：windows主机，已跟云服务器互通。云服务器(其中公网IP一个，内网IP五个)

需求：需要上传若干GB级文件到云服务器上的hdfs存储。

问题：

hdfs WebUI，可以正常访问，上传、删除文件夹，删除文件，但是不能上传文件。

报错提示：

文件上传不了，`woker3`是我的内网节点名字，可以发现是解析不成功。
![image](https://github.com/deliciousteas/Note/assets/107855849/a9d826a3-474d-42ba-aa51-f611982bca3a)


![image](https://github.com/deliciousteas/Note/assets/107855849/f96cf090-61b7-442c-ba3f-c512a262bab0)





解决方案：

hdfs通过9864端口访问，在浏览器中发现hdfs报错是域名，而不是IP地址（这些是内网IP无法外网访问）。

实际上namenode我绑定了公网IP可以访问，而我的剩下datanode是内网IP，它的9864端口无法完成到本地windows机器的端口映射。所以直接绑定个公网IP就行。

所以在服务器买了公网IP，绑定个woker1，然后在本地电脑上修改etc/host ，如下：

新买的公网IP：woker1

新买的公网IP：woker2

.....

然后就可以了。

## 问题总结

文件上传问题：

**权限配置问题或者数据节点的访问限制。**

- 权限问题在hdfs-site.xml和core-site.xml文件中设置访问权限和验证权限。
- 数据传输权限，确保数据节点的访问限制正确配置，允许通过公网IP进行数据传输。

端口映射问题：

* 防火墙一方面，格挡了局域网或者公网IP访问。
* 网络设备的配置，数据节点的内网IP无法与公网访问。

>EIP() Elastic IP Address) 通过EIP与公网通信。
>
>端口映射：将内网中的host的port映射到外网主机的一个端口，提供服务。

# 其他尝试方案

* 上传到服务器，再上传到hdfs
  * Winscp
* 上传到Nas，再上传到hdfs
  * WebDav
* 直接上传到hdfs
  * windows环境挂载在linux环境
  * hdfs webUI 访问
    * 设置防火墙
* hdfs：修改hdfs-site.xml文件
  * 无影响，我本身能够远程访问hdfs webUI界面然后也可以创建，说明权限没问题。
* windows硬盘挂载到linux上：遭运维大哥否定。
* windows防火墙
  * 根据公网IP所在地址和端口，设置in and out规则
