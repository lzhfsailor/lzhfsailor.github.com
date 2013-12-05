---
layout: post
title: 函数式编程
category: wiki
description: wiki of FP
---

##高阶函数

* 函数抽象：

<pre>
    // 一个小例子，显然有重复的代码：

    alert("I'd like some Spaghetti!");
    alert("I'd like some Chocolate Moose!");
    
    //进行函数层次的抽象
    function SwedishChef( food )
    {
        alert("I'd like some " + food + "!");
    }
    SwedishChef("Spaghetti");
    SwedishChef("Chocolate Moose");
</pre>

* 高阶函数抽象：

<pre>
    //一个小例子，显然有重复的代码
    alert("get the lobster");
    PutInPot("lobster");
    PutInPot("water");

    alert("get the chicken");
    BoomBoom("chicken");
    BoomBoom("coconut");
    
    //使用函数+高阶函数进行抽象
    function Cook( i1, i2, f )
    {
        alert("get the " + i1);
        f(i1);
        f(i2);
    }
    Cook( "lobster", "water", PutInPot );
    Cook( "chicken", "coconut", BoomBoom );
    
    //还可以使用一个语法糖——匿名函数使他简洁化
    Cook( "lobster", 
          "water", 
          function(x) { alert("pot " + x); }  );
    Cook( "chicken", 
          "coconut", 
          function(x) { alert("boom " + x); } );
</pre>

有了高阶函数后，还可以对“遍历”进行抽象：

<pre>
    //原来只能这样：
     var a = [1,2,3];

    for (i=0; i<a.length; i++)
    {
        a[i] = a[i] * 2;
    }

    for (i=0; i<a.length; i++)
    {
        alert(a[i]);
    }
    
    //现在可以这样：
    function map(fn, a)
    {
        for (i = 0; i < a.length; i++)
        {
            a[i] = fn(a[i]);
        }
    }
    map( function(x){return x*2;}, a );
    map( alert, a );
</pre>

有了对“遍历”的抽象之后有什么好处呢？由于这个遍历是对处理顺序不敏感的，我们可以找一个牛人写一个多线程的map进行并行处理，而其他人只需要调用map。

##闭包

在计算机科学中，闭包（Closure）是词法闭包（Lexical Closure）的简称，是引用了自由变量的函数。这个被引用的自由变量将和这个函数一同存在，即使已经离开了创造它的环境也不例外。所以，有另一种说法认为闭包是由函数和与其相关的引用环境组合而成的实体。

Peter J. Landin 在1964年将术语闭包定义为一种包含环境成分和控制成分的实体。

举个例子：

<pre>
var fn = (function(){
    var a = "super long string...";
    var b = "useless value";
    var c = "Hello, world!";
        
    return fuction(){
        return c;
    };
})();
</pre>

代码执行后fn被赋值为一个函数，这时调用fn，能不能得到c呢？答案是肯定的，虽然这时函数体的代码已经执行完毕，c的作用域早就结束了，但是由于闭包的特性，fn能访问到c。

再举一个Node.JS的例子：

<pre>
function main(){
    var id = "1";
    db.query("select name from persons where id=" + id,function(name){
        output("person id:" + id +", name:" + name);//n秒后返回数据执行回调函数
        });
}
</pre>

我们注意到，main执行到db.query的时候就丢给它处理然后继续向下执行了。当db.query执行了几秒钟取得结果之后，main函数已经结束了。这时就有一个问题：db.query这时仍然想用原来main函数里面的id属性（这个属性现在早就走过了作用域了）。这个id属性现在还存在吗？答案是存在，这同样归功于JavaScript的闭包特性。

* 闭包特性有可能造成内存浪费，解决的方法一般分为：
    
    > 编程手段：手动释放掉内存;在可能闭包的函数中不声明不必要的属性；
    
    > JavaScript解释引擎的优化；
    
    > 静态编译；
    
##λ演算

λ演算（lambda calculus）是一套用于研究函数定义、函数应用和递归的形式系统。

它由Alonzo Church 和 Stephen Cole Kleene在20世纪30年代引入

* 使用BNF范式定义：

    <expression>::=<name>|<function>|<application>

    //表达式定义
    
    < function >::=λ < name >.< expression > 
    
    //函数抽象:用来生成函数。例： λ x. x+3
    
    < application >::=(< expression > < expression >)
    
    //函数作用:使函数作用于参数。例： λ x. x+3 4 =>7
    
* 公理：
    
    α-置换公理： λ x y. x+y == λ a b. a+b
    
    β-归约公理： (λ x y. x+y) a b => a+b
    
[π演算PPT](http://www.doc88.com/p-619602863113.html)

##柯里化

为尽量精简，lambda算子只接受一个参数。那怎么处理多个参数呢？

    Func<int, Func<int, int>> f = x => y => x + y;
    
    int i = f(1)(2);

f 等于这样一个函数，接受一个int参数x，并返回另一个函数Func<int, int>，这个函数再接收一个int参数y，且对这个函数的调用结果是x + y

##尾递归



[C#和Java的闭包－Jon谈《The Beauty of Closures》](http://www.cnblogs.com/jeriffe/articles/1733157.html)

[Inversion of Control Containers and the Dependency Injection pattern](http://martinfowler.com/articles/injection.html)


[函数式思维: 大量转换](http://www.ibm.com/developerworks/cn/java/j-ft16/)

[函数式程序设计为什么至关重要](http://www.byvoid.com/blog/why-functional-programming/)

[尾递归对时间与空间复杂度的影响](http://blog.zhaojie.me/2011/11/does-tail-recursion-improve-time-and-space-complexities-1.html)

[手把手教你做λ](http://a.haskellcn.org/topic/4f9e4037edefd68d37010c8b)

[递归函数](http://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92%E5%87%BD%E6%95%B0)


