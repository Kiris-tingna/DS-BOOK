[TOC]

# 第三章 聚类与衡量方式
> Markdown Revision 1

> Date: 2018/12/05

> Editor: kirisitngna

> Contact: https://www.github.com/Kiristingna



## 3.1 聚类好坏的判定

##### A.基于聚类簇的判定

假设$P=\{P_1, P_2, \dots, P_s\}$ 是人工判定的分类结果集$C=\{C_1, C_2, \dots, C_m\}$ 是算法得到的结果集，一个样本只能属于一个簇。对于每个人工标注的簇 $P_j$, 假设在$C$ 中都有唯一与之对应的簇 $C_i$， 这个对应关系是未知的。那么首先应该确定两两簇之间的准确率，召回率， F值，聚类整体加权F值（F_class）
$$
P(C_i, P_j) = \frac{|P_i \bigcap C_i|}{|C_i|} ~~ 
R(C_i, P_j) = \frac{|P_i \bigcap C_i|}{|P_j|}\\
F(C_i, P_j) = \frac{2PR}{(P+R)} ~~
F(C_i) = \max_{1 \leq j \leq s} F(C_i, P_j)\\
F_{class} =\sum_{i=1}^m\frac{|C_i|}{n} \cdot F(C_i)
$$
相当于从$P$ 当中选取一个与之最接近的簇$P_j$, 该指标综合考虑了准确率和召回率。这个指标的缺点是 对于大类可能不能很好地反应聚类好坏。

##### B.基于数据对象的判定

假设$P_x$ 是 $P$中 $x$ 数据对应的聚类对象, 假设$C_x$ 是 $C$中 $x$ 数据对应的聚类对象, 那么
$$
P(x) = \frac{|P_x \bigcap C_x|}{|C_x|} ~~ 
R(x) = \frac{|P_x \bigcap C_x|}{|P_x|}\\
F(x) = \frac{2PR}{(P+R)} ~~
\\
F_{class} =\frac{1}{n} \sum_{i=1}^n\cdot F(x_i)
$$
实验中发现 基于对象的平均准确率

##### C.熵

定义
$$
En(C_i) = \frac{1}{log (s)} \sum_{j=1}^s\frac{|C_i\bigcap P_j|}{|C_i|}log \frac{|C_i|}{|C_i\bigcap P_j|} 
$$
熵不仅仅可以单独评估一个簇，也可以利用簇的大小进行加权平均对整个聚类结果进行评价，熵的特点是偏好小类。实际情况中使用熵，必须结合类的F值进行整体评价。

