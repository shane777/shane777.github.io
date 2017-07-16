---
layout: post
title:  "前端模块化"
date:   2017-07-16 13:56:48 +0800
categories: HTML
---
在学node.js, 实际上就是基于common.js开发的，所以了解了一下模块化开发。

JS的模块化初衷和所有语言的模块化都是一致的，就是规范化开发。


	1. 最早期的时候就是原生的js从上到下代码编写执行，
	
	{% highlight ruby %}
	function fun1(){ //... }
	function fun2(){ //... }
	{% endhighlight %}
	
	所有的函数和变量都直接放入相应的js文件中。导致的问题就是全局对象Global被污染，函数命名冲突。同时在js文件之间有所依赖时，还要保证文件引入的顺序，文件之间的依赖关系不好管理。
	
	
	2. 为了解决上面的问题，采用了使用对象封装的模式。
	
	{% highlight ruby %}
	var module1 = { 
		property1 : 1,
		property2 : 2,
		fun1 : function(){}, 
		fun2: function(){}
	}
	obj.fun1();
	{% endhighlight %}
	
	好处是减少了对全局对象的污染，而新的问题是对象类型的不安全，在外部可以对其内部进行修改。
	
	
	3. 而采用匿名闭包就可以达到隐藏其内部细节的功能。
	
	{% highlight ruby %}
	var module1 =( function () { 
		var property1 = 1;
		var property2 = 2;
		function fun1(){};
		function fun2(){};
		return { fun1: fun1, fun2: fun2};
	}) ();
	module1.fun1();
	module1.property1 ; // undefined
	{% endhighlight %}
	
	
	4. 而考虑到依赖，一种比较典型的方法是JQuery封装风格。

	{% highlight ruby %}
	(function(window){
	    //代码
	    window.jQuery = window.$ = jQuery;//通过给window添加属性而暴漏到全局
	})(window);
	{% endhighlight %}

	通过匿名函数包装代码，所依赖的外部变量传给这个函数，在函数内部可以使用这些依赖，然后在函数的最后把模块自身暴漏给window。
	如果需要添加扩展，则可以作为jQuery的插件，把它挂载到$上。
	这种风格虽然灵活了些，但并未解决根本问题：所需依赖还是得外部提前提供、还是增加了全局变量。
	
	
	5. 而最后一个问题，文件的加载。 过多的<script>标签引入文件导致请求过多，加载顺序的固定，平行加载，导致依赖之间的模糊。所以之后出现了LAB.js这种script loader 还有 module loader YUI3等。实际上因为浏览器端任务量较小的缘故，各种复杂的JS逻辑也可以执行下去。但是进入到了服务器端以后，更迫切的需要模块化的存在。

  ##1.CommonJS规范
   
	CommonJS是服务器端模块的规范，Node.js采用了这个规范。Node.JS首先采用了js模块化的概念。
	根据CommonJS规范，一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为global对象的属性。
	输出模块变量的最好方法是使用module.exports对象。
	
	{% highlight ruby %}
	var i = 1;
	var max = 30;
	module.exports = function () {
	  for (i -= 1; i++ < max; ) {
		console.log(i);
	  }
	max *= 1.1;
	};
	{% endhighlight %}
	
	上面代码通过module.exports对象，定义了一个函数，该函数就是模块外部与内部通信的桥梁。
	加载模块使用require方法，该方法读取一个文件并执行，最后返回文件内部的module.exports对象。
	
	
  ##2. AMD
  
	AMD 即Asynchronous Module Definition，中文名是异步模块定义的意思。它是一个在浏览器端模块化开发的规范。
	模块将被异步加载，模块加载不影响后面语句的运行。所有依赖某些模块的语句均放置在回调函数中。
	由于不是JavaScript原生支持，使用AMD规范进行页面开发需要用到对应的库函数，也就是大名鼎鼎RequireJS，实际上AMD 是 RequireJS 在推广过程中对模块定义的规范化的产出
	requireJS主要解决两个问题
		1. 多个js文件可能有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
		2. js加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应时间越长
	看一个使用requireJS的例子
	
	{% highlight ruby %}
	// 定义模块 myModule.js
	define(['dependency'], function(){
		var name = 'Byron';
		function printName(){
			console.log(name);
		}
		return {
			printName: printName
		};
	});
	// 加载模块
	require(['myModule'], function (my){
		my.printName();
		});
	{% endhighlight %}
	
	requireJS定义了一个函数 define，它是全局变量，用来定义模块
	
	`define(id?, dependencies?, factory);`
	
	1. id：可选参数，用来定义模块的标识，如果没有提供该参数，脚本文件名（去掉拓展名）
	2. dependencies：是一个当前模块依赖的模块名称数组
	3. factory：工厂方法，模块初始化要执行的函数或对象。如果为函数，它应该只被执行一次。如果是对象，此对象应该为模块的输出值
	
	{% highlight ruby %}
	 define("alpha", ["require", "exports", "beta"], function (require, exports, beta) {
       exports.verb = function() {
           return beta.verb();
           //Or:
           return require("beta").verb();
       }
   });
	{% endhighlight %}	
	
	在页面上使用require函数加载模块
	
	`require([dependencies], function(){});`
	
	require()函数接受两个参数
	1. 第一个参数是一个数组，表示所依赖的模块
	2. 第二个参数是一个回调函数，当前面指定的模块都加载成功后，它将被调用。加载的模块会以参数形式传入该函数，从而在回调函数内部就可以使用这些模块
	require()函数在加载依赖的函数的时候是异步加载的，这样浏览器不会失去响应，它指定的回调函数，只有前面的模块都加载成功后，才会运行，解决了依赖性的问题。

	
	##3.CMD
	
	CMD 即Common Module Definition通用模块定义，CMD规范是国内发展出来的，就像AMD有个requireJS，CMD有个浏览器的实现SeaJS，SeaJS要解决的问题和requireJS一样，只不过在模块定义方式和模块加载（可以说运行、解析）时机上有所不同。实际上本身Seajs就是通过学习并通过其自己的习惯改良成的。
	在 CMD 规范中，一个模块就是一个文件。代码的书写格式如下：
	
	`define(factory);`
	
	factory 为函数时，表示是模块的构造方法。执行该构造方法，可以得到模块向外提供的接口。factory 方法在执行时，默认会传入三个参数：require、exports 和 module：
	
	{% highlight ruby %}
	define(function(require, exports, module) {
	// 模块代码
	});
	{% endhighlight %}
	
	##4.AMD与CMD的区别
	
	所有的资料都会告诉你区别是CMD 推崇依赖就近，AMD 推崇依赖前置。实际上依赖就近的含义就是随用随require，而依赖前置的意思就是这一段define需要什么全部在一开始的地方require完毕。
	
	{% highlight ruby %}
	// CMD
	define(function(require, exports, module) {
	var a = require('./a')
	a.doSomething()
	//...
	var b = require('./b') // 依赖可以就近书写
	b.doSomething()
	// ... 
	})
	// AMD 默认推荐的是
	define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
	a.doSomething()
	// ...
	b.doSomething()
	...
	}) 
	{% endhighlight %}
	
	但两者都是异步操作的。
	
		
   5. ES6模块标准
	实际上模块化已经开始纳入ES标准了， 相应的ES Module部分才是建议仔细学习的地方。以后应该会向此靠拢的。
	----------------------------------------
	参考：
	http://www.cnblogs.com/dolphinX/p/4381855.html
	https://segmentfault.com/a/1190000000733959#articleHeader1
	http://www.cnblogs.com/lvdabao/p/js-modules-develop.html
	
