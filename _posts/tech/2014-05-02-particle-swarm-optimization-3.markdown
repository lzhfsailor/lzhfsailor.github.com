---
layout: post
title:  "粒子群优化算法（三）：应用"
date:   2014-05-02 14:39:56 
categories: [tech,pso]
description: 本文将详细解读粒子群算法在求解TSP问题上的应用

---
本文将详细解读粒子群算法在求解TSP问题上的应用
# 问题描述 #

----------
+ TSP问题（Travelling Salesman Problem）即旅行商问题。假设有一个旅行商人要拜访n个城市，他必须选择所要走的路径，路径的限制是每个城市只能拜访一次，而且最后要回到原来出发的城市。路径的选择目标是要求的路径路程为所有路径之中的最小值。
+ 采用Java语言编程实现
+ 代码同步到github上：[粒子群优化求TSP问题](https://github.com/lzhfsailor/EAs/tree/master/EAs/ "粒子群优化求TSP问题")

# 程序实现 #
V={c1, c2, …, ci, …, cn}，i = 1,2, …, n，是所有城市的集合.ci表示第i个城市，n为城市的数目；E={(r, s): r,s∈ V}是所有城市之间连接的集合；C = {crs: r,s∈ V}是所有城市之间连接的成本度量（一般为城市之间的距离）；
如果crs = csr, 那么该TSP问题为对称的，否则为非对称的。一个TSP问题可以表达为：求解遍历图G = (V, E, C)，所有的节点一次并且回到起始节点，使得连接这些节点的路径成本最低。

----------

<input type=image  value=show&hide src="/images/hide.ico"  width ="20" height="20" onclick=display(codeHide)> 单击隐藏或显示代码
<div id=codeHide>
{% highlight java %}
 
{% endhighlight %}
</div>
----------
# 结果分析 #



