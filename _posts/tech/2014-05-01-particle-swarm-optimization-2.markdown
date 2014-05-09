---
layout: post
title:  "粒子群优化算法（二）：实现"
date:   2014-05-01 11:21:21 
categories: [tech,pso]
description: 本文将用求解函数最大值的例子来实现粒子群算法
---
本文将用求解函数最大值的例子来实现粒子群算法
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
 package simplePSO;
 import java.util.Random;
 /**
  * Copyright &reg; 2014 Jinan
  * 
  * @description v[i] = w * v[i] + c1 * rand() * (pbest[i] - present[i]) + c2 *
  *              rand() * (gbest - present[i]);present[i] = present[i] + v[i]
  * @author Heming.Liang
  * @version 1.0 粒子群优化算法求解y=-x*(x-2) 在[-2,2]上最大值 All right reserved.
  */
 public class Maximum {
 	int n = 2; // 粒子个数
 	double[] y;// 粒子位置
 	double[] x;// 粒子取值
 	double[] v;// 粒子更新速度
 	double c1 = 2;
 	double c2 = 2;
 	double pbest[];// 粒子历史最好位置
 	double gbest;// 全局最优位置
 	double vmax = 0.1;// 设置速度最大值
 	public void fitnessFunction() {// 适应函数
 		for (int i = 0; i < n; i++) {
 			y[i] = -1 * x[i] * (x[i] - 2);
 		}
 	}
 	public void init() { // 初始化
 		x = new double[n];
 		v = new double[n];
 		y = new double[n];
 		pbest = new double[n];
 		/***
 		 * Math.random()产生0-1之间类型为double的随机数
 		 */
 		for (int i = 0; i < n; i++) {
 			x[i] = Math.random() * 4 - 2;
 			v[i] = x[i] > vmax ? vmax : x[i];
 		}
 		fitnessFunction();
 		// 初始化当前个体极值，并找到群体极值
 		for (int i = 0; i < n; i++) {
 			pbest[i] = y[i];
 			if (y[i] > gbest)
 				gbest = y[i];
 		}
 		System.out.println("start gbest:" + gbest);
 	}
 	public void PSO(int max) {
 		for (int i = 0; i < max; i++) {
 			double w = 0.4;
 			for (int j = 0; j < n; j++) {
 				// 更新位置和速度
 				v[j] = w * v[j] + c1 * Math.random() * (pbest[j] - x[j]) + c2
 						* Math.random() * (gbest - x[j]);
 				if (v[j] > vmax)
 					v[j] = vmax;
 				x[j] += v[j];
 				// 越界判断
 				if (x[j] > 2)
 					x[j] = 2;
 				if (x[j] < -2)
 					x[j] = -2;
 			}
 			fitnessFunction();
 			// 更新个体极值和群体极值
 			for (int j = 0; j < n; j++) {
 				pbest[j] = y[j] > pbest[j] ? y[j] : pbest[j];
 				if (pbest[j] > gbest)
 					gbest = pbest[j];
 				System.out.println(x[j] + "  " + v[j] + "  " + y[j]);
 			}
 			System.out.println("======generation " + (i + 1) + "======gbest:"
 					+ gbest);
 		}
 	}
 	public static void main(String[] args) {
 		Maximum ts = new Maximum();
 		ts.init();
 		ts.PSO(1000);
 	}
 }
{% endhighlight %}
</div>
----------
# 结果分析 #

粒子群算法没有选择交叉变异等进化计算所具有的过程，所以实现起来比较容易，但很容易陷入局部最优。所以，<span class="strongFont">可以在粒子群算法中加入变异等方便跳出局部最优的方法，来得到更好的解</span>。

