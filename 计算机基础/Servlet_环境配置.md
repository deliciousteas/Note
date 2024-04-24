> 服务器上安装企业或者ultimate版本以上的idea，然后根据java版本安装tomcat。

## Servlet

**@WebServlet**：将java类声明为Servlet类

* 在下图中name属性可以指定Servlet名称
* value是指定Servlet监听的URL规则，只监听用户以value结尾的路径。

![image](https://github.com/deliciousteas/Note/assets/107855849/7353ddc1-e2c9-4299-a7bd-6dd252be55a0)


**method**(GET POST)

处理客户端的HTTP的get和post请求。

* HttpServletRequest：客户端的HTTP请求
* HttpServletResponse：服务器向客户端发送的HTTP响应

## Tomcat配置：idea

run/debug configuration进入，然后设置该server的类型和name，我test的是在本地。

* Application server：tomcat的bin路径。
* open browser：可以选择浏览器类型，URL可以设置默认初始化界面
* tomcat Server Settings：Http port，8080端口我的被spark用了，8081被tomcat用了，就用的8082
  * JMX:应用程序的端口，查看程序的状态。

![image](https://github.com/deliciousteas/Note/assets/107855849/936eb14d-60ec-4d8c-8391-525fa379aaeb)


## web.xml参数

servlet-mapping设置路径

![image-20240423191738506](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240423191738506.png)

**jsp文件**：javaServer Pages 动态网页技术标准，可以根据请求返回生成HTML或者其他web网页，相当于在HTML中嵌入的ljava代码，HTML侧重静态数据展示。

serverlet工作流：

s01是project，ser001是一个模块运行。

![image](https://github.com/deliciousteas/Note/assets/107855849/6c4a84f4-33f2-44e4-bf13-66a184e2a8cb)


500是服务器设置错误

404网页错误

servelet可以约束get或者post方法

> ?连接域名和参数
>
> &不同参数之间连接

# 参考

[webServlet注解](https://blog.csdn.net/nxj_climb/article/details/117193250)

[idea web添加application servers](https://blog.csdn.net/uncle_david/article/details/83989436)

[idea配置本地Servlet](https://blog.csdn.net/m0_61105833/article/details/127135431)

[servlet-mapping参数](https://www.cnblogs.com/yanze/p/10457924.html#:~:text=%E5%B0%86URL,%E8%AF%A5Servlet%E5%A4%84%E7%90%86%E7%9A%84URL%E3%80%82&text=%E5%AE%B9%E5%99%A8%E7%9A%84Context%E5%AF%B9%E8%B1%A1%E5%AF%B9,%E8%B0%83%E7%94%A8%E8%BF%99%E4%B8%AAServlet%E5%A4%84%E7%90%86%E8%AF%B7%E6%B1%82%E3%80%82)

[网页连接符](https://blog.csdn.net/wx912820/article/details/104829630#:~:text=%23%E4%BB%A3%E8%A1%A8%E7%BD%91%E9%A1%B5%E4%B8%AD%E7%9A%84%E4%B8%80%E4%B8%AA,%E5%AF%B9%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%AE%8C%E5%85%A8%E6%97%A0%E7%94%A8%E3%80%82)
