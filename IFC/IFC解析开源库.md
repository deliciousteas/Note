# IFC解析开源库| c++ |java

> 最近要做IFC研究，收集相关IFC解析开源库，供研究选择，欢迎研究IFC的友友互相交流学习
# IFC定义
IFC是一种数据模型，基于类定义的面向对象数据模型，关注共享信息的类（而不是软件操作类）
# IFC版本
ifc1.0、1.5、1.51，2x，2x2、2x3；其中2011推出IFC2X4（也称为IFC4）
# IFC文件形式
.ifc：基于 ISO STEP 物理格式 (SPF) 标准的默认文件格式  
.ifc-xml : 基于 XML 语言的编码  
.ifc-zip：这些格式之一的压缩档案  
# IFC解析工具
1. xbim
编程语言：c#为主，几何引擎是用c++；  
IFC版本：FC2X3, IFC4, IFC4，IFC4X1  
IFC格式：IFCxml、ifc、ifczip  
开源情况：开源  
2. ifcopenshell
编程语言：c草/python都可以  
IFC版本：IFC2X3、IFC4、IFC4x1 、IFC4x2  
IFC格式：.ifc  
开源情况：开源  
3. sikongsphere-ifctools 0.02beta  
编程语言：java  
IFC版本：IFX2X3  
IFC格式：.ifc  
开源情况：开源  
4. ifcplusplus 
编程语言：c++  
开源情况：不开源  
5. apstex IFC Framework  
编程语言：java  
开源情况：学术免费用，部分开源  
6. bimserver  
编程语言：前端  
# 总结
* 主要以c++为主，其中ifcopenshell支持python操作，但是考虑到大批量数据使用python会有性能限制，选择c++和python根据情况来看。  
* java语言的开源库较少，最新的司空学社java仅支持IFC2X3，另一部分apstex IFC Framework网络上教程也较少。  
* 如果需要做可视化效果，数据量不大，可以考虑基于bimserver，它是基于网页传输加载的。  
