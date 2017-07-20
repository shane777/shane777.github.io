---
layout: post
title:  "JavaScript异步与回调函数"
date:   2017-07-20 12:55:00 +0800
categories: Javascript
---
常见的同步和异步概念如下：
同步：即传统的代码从上到下执行。
异步：前一个方法未全部执行完毕的时候下一个方法就可以开始执行。

Javascript是一门单线程语言，实际上并不能实现一般语言意义上的非阻塞异步，即一段程序因为耗时较长未能运行完毕时其他程序也可以继续运行。

JavaScript 的异步是一种伪异步，实际上是通过延迟执行实现的，比如setTimeout。还有就是事件驱动执行，实际实现方法就是注册事件，绑定回调函数，事件发生时调用对应的回调函数的过程。相当于将一部分未完成的任务先储存起来，到合适的时机再执行。

javascript的好处是其线程的执行是异步的，因为当执行这个回调函数的时候，可能js引擎正在从上到下的执行代码，也可能已经进入空闲。异步代码会被放入一个事件队列，等到所有其他代码执行后才进行，而不会阻塞线程。

回调函数这个名字实在是过于暧昧，以至于理解上容易出现误差。其实叫做“当事件发生时需要调用的函数”比较好。不过大概这个名字又太长了。
如果举现实中的例子，它大概就是相当于你去商店里买东西，恰好没货，你告诉售货员等有货给你打电话。这个过程中给你打电话就是回调函数。

其具体实现一般如下：

```JavaScript
function1 (){
  //some action
}
function2 (callback){
  //..some action
  callback();
}
function2(function1);
```

在这里，function1就是回调函数。实际上在setTimeout(function,time)中我们传进去的function也是回调函数。

举个事件驱动的例子

```JavaScript
var http = require("http")
function onRequest(request,response){
    console.log("");
    //maybe some action....
}
//登记回调函数
http.createServer(onRequest).listen(8888);
```


在以上代码中onRequest就是回调函数，createServer这个函数就是在登记回调函数。当端口监听到8888的时候就会调用这个回调函数。

关于更多异步编程的实现方法推荐阅读文章
http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html
