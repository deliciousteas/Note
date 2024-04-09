# 摘要

城市空间测度中，城市人群移动的异质性主要受城市空间尺度结构的影响。

社交媒体大数据可以使我们更深入地了解人类移动行为。本文亦在利用带有地理标记地twitter blog和伦敦、东京街道路网来探索影响人类迁移模式的机制。

对于连个城市，通过处理数十万条tweet位置和路网，生成城市热点区域和自然街道。然后利用用户移动轨迹和城市热点区域构建一个可以定量表征城市内人群移动的网络。为了模拟观测到的移动模式，该研究进行了一个基于两层代理的模拟，其中中包括通过网络的随机游走和三种距离类型的网络移动模式。

# 方法：

* 轨迹数据：按照时间顺序提取每个用户的轨迹，通过聚类获取热点区域。然后由热点区域的地点作为节点，节点之间的用户流动表示为Edge。
  * 基于Agent仿真，对热点网络生成随机轨迹。
* 路网角度：考虑了metric，angle and distance

## 数据：预处理与聚类(数据预处理、完成聚类)

id、xy坐标、时间戳。

1. 剔除预处理，选一个处理标准作为背书。(Wu et al.(2014),Shen et al(2019))
2. Tin三角形聚类，(Jiang 2017 ...提出基于Tin的不规则三角网空间聚类方法)
3. 将用户之间的移动聚类到热点之间的移动，于是得出有向加权的热点网络。

## 实验模拟：2层人类行为模型测试

RandWalk： hotspot network

* 人类群体移动行为可以通过假定Agent的每一次动作和状态受到马尔科夫链的影响，ABM在可以hotsport中通过随机游走获取该agent稳定后的状态分布情况。

Street movement simulation

把热点替换为热点区域的segment，segment到热点视为1到多的概率事件。

然后将segment的组成视为network，其中node为individual segment,Edge 为intersected segments relationship,其中edge可以加权(metric，angle、distance)。

考虑到OD之间使用什么加权的情况：个体在找路时会被认为时metric and angular distance 的合计。

## 数据解释与分析

scaling analysis(标度分析....)

power law distributions 幂律分布，Head/tail breaks和inductive ht指数也是描述异质性水平的指标，作为有效补充。

幂律的不同等价于维度的不同，维数越高，幂律的数值也越大，当然幂律的dimension可以是任何数，于是产生了分形的概念。

![image-20240409193121415](C:\Users\22779\AppData\Roaming\Typora\typora-user-images\image-20240409193121415.png)

> 幂律 power law,是描述两个变量之间的函数关系，自变量的变化会导致另一个变量的变化成幂次方，其中与初始值无关。
>
> 幂次方：a的N次方，即a的N次幂
>
> 指数：exponentials
>
> 无标度网络：标度改变时，函数曲线的形状和函数的指数都没有变化，具有标度不变性。(Scale-free/scale-invariant)
>
> Head/tail breaks 是一种具有长尾分布的聚类方法。小数据远多于大规模数据,由此聚类算法产生的class指数称为ht指数，表征分形维数。其中ht越大，分形越复杂。
>
> 齐普夫定律是幂律分布的特殊表现。

# Sum

科学问题：人类活动异质性(Heterogeneity of human urban movements)-城市空间尺度结构对人类活动异质性影响的机制。

该文围绕城市空间尺度对于人类移动行为的影响展开，重点解释了城市内人群的移动模式、分布规律以及移动行为的驱动因素，并解释了城市人群移动的异质性。

>  备注:
>
> **Agent:a colletion of autonomous decision-making entites.**
>
> 通过ABM规避了数据中假设人群中的同质化，避免了以极端的人群画像刻画，ABM承认个体之间的异质性，是相较于假定条件上的一种进步。
>
> heterogeneity 异质
>
> heterogeneous 异构
>
> **马尔科夫链：**
>
> * 马尔可夫链是描述一系列状态之间的转移概率，未来只取决于当前状态。
> * 权重之和一定为一。
> * 长时间状态转移后，状态分布区域稳定的概率分布。于是可以用来预测系统行为。
>
> **空间句法：影响人类活动行为，包括城市环境(路网)和个体移动行为(OD数据)**
>
> * 城市环境：复杂网络理论提供测度方法
>   * 从测度来讲，城市空间往往呈现幂律分布和长尾分布。
> * 个体移动行为：最短路径，包括从长度、角度、方位三种方式的最小测量手段
>   * 最短路径取决于个体的空间认知水平。

# 参考

[Exploring the heterogeneity of human urban movementsusing geo-tagged tweets](https://www.tandfonline.com/doi/epdf/10.1080/13658816.2020.1718153?needAccess=true)

[基于代理的模型，ABM](https://wiki.swarma.org/index.php/%E5%9F%BA%E4%BA%8E%E4%B8%BB%E4%BD%93%E7%9A%84%E6%A8%A1%E5%9E%8B_Agent-based_model)

[马尔科夫链](https://blog.tangly1024.com/article/markov-chain)

[幂律之于城市](https://www.sohu.com/a/274492710_741733)

[什么是幂律](https://necsi.edu/power-law)

[什么是幂律分布：视频版](https://www.bilibili.com/video/BV1u14y1f7Cq/?spm_id_from=333.337.search-card.all.click&vd_source=b61ce8d81a5e8e82447077f84ae7352a)

[Head/tail breaks](https://en.wikipedia.org/wiki/Head/tail_breaks)