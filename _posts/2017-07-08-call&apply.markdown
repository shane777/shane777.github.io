---
layout: post
title:  "call apply以及相应的问题!"
date:   2017-07-08 18:18:13 +0800
categories: Javascript
---
基础定义：每个函数都包含两个非继承而来的方法：apply()和call()。这两个方法的用途都是在特定的作用域中调用函数，实际上也可以说all 和 apply 是为了动态改变 this 而出现的，当一个 object 没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。


apply()：接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是Array实例，也可以是arguments对象。

Call()：与apply()方法作用相同，区别在于接收参数的不同，第一个依旧是this值，而要传递给函数的参数必须逐个列举出来。所以一般在明确知道参数数量时使用。

即apply方法的第二个参数接受一个数组,数组里面的每个元素会被当成参数逐个传进。call方法除了第一个参数之外的多个参数会被当成参数逐个传进。

相应题目思考：
有一道经典的面试题是这样的
{% highlight ruby %}
function log(){
  console.log.apply(console, arguments);
};
log(1);   //1
log(1,2);   //1 2
{% endhighlight %}


与直接调用 console.log(arguments)的区别是 后者会将arguments作为数组打印出来
![screenshot1]({{site.url}}/assets/170708_1.png)

查阅了一些资料得出结论是这是由apply特性决定的，apply接收的是一个数组，并会将其转变参数列表打印出来。

更有趣的一个问题（来源segmentfault）：
![screenshot2]({{site.url}}/assets/170708_2.png)

![screenshot3]({{site.url}}/assets/170708_3.png)

因为apply把数组拆分成了独立的参数传入，相当于txt=yellow，而orgen没有相应的变量名接收,而call把推进来的数组当作一整个参数赋值给了newArray,push不接受数组形式.

//改成this.key.concat(txt)

//或者this.key.apply(this.key , txt)也可以
