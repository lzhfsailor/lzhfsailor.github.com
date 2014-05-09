---
layout: post
title:  "粒子群优化算法（三）：应用"
date:   2014-05-02 14:39:56 
categories: [tech,pso]
description: 本文将详细解读粒子群算法在神经网络优化等方面的应用
---
本文将详细解读粒子群算法在神经网络优化等方面的应用
# 问题描述 #

----------
+ 求解y=-x*(x-2) 在[-2,2]上最大值
+ 采用Java语言编程实现
+ 代码同步到github上：[粒子群优化求函数最大值](https://github.com/lzhfsailor/EAs/tree/master/EAs/src/simplePSO "粒子群优化求函数最大值")

# 程序实现 #

----------
<input type=image  value=show&hide src="/images/hide.ico"  width ="20" height="20" onclick=display(codeHide)> 单击隐藏或显示代码
<div id=codeHide>
{% highlight java %}
 
{% endhighlight %}
</div>
----------
# 结果分析 #

粒子群算法没有选择交叉变异等进化计算所具有的过程，所以实现起来比较容易，但很容易陷入局部最优。所以，<span class="strongFont">可以在粒子群算法中加入变异等方便跳出局部最优的方法，来得到更好的解</span>。

