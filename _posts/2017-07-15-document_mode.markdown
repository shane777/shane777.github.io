---
layout: post
title:  "文档模式与文档类型"
date:   2017-07-15 21:19:33 +0800
categories: HTML
---
读到js高程第十一章，对文档模式和文档类型的区别有点疑问，做了一番搜索和书的再阅读，总结了一下。

页面的文档模式决定了可以使用什么功能，换句话就是说，文档模式决定了你可以使用哪个级别的CSS，可以在javascript中使用哪些API，以及如何对待文档类型(doctype)。
HTML的文档模式可以通过使用文档类型DOCTYPE来指定的。在所有 HTML 文档中规定 DOCTYPE 是非常重要的，这样浏览器就能了解预期的文档类型， 告诉浏览器要通过哪一种规范解析文档（比如HTML或XHTML规范）。
HTML 4.01 中的 doctype 需要对 DTD 进行引用，因为 HTML 4.01 基于 SGML。而 HTML 5 不基于 SGML，因此不需要对 DTD 进行引用，但是需要 doctype 来规范浏览器的行为。


目前文档模式有三种：混杂模式（quirks mode）、标准模式（standards mode/ strict）和准标准模式。对于准标准模式，一般又是通过过渡型（transitional）和框架集型（frameset）来触发。这些对于HTML 4.01 中的 doctype都会有不同的类型和DTD，而HTML5都是统一的<!doctype html>

文档模式也会被<meta http-equiv="X-UA-Compatible">影响，这个标签的含义是强制浏览器以某种模式渲染页面。
<meta http-equiv="X-UA-Compatible" content = "IE=IEVersion">
1. IE=5：强制将文档模式设置为IE5，忽略文档类型生命，采用quirks模式；
2. IE=7/8/9：表示采用对应IE版本的标准模式，忽略文档类型声明，使用标准模式；
3. IE=EmulateIE7/EmulateIE8/EmulateIE9，采用模拟对应IE版本的模式，如果是以<!DOCTYPE>作为文档第一行则采用该版本的标准模式，否则将文档模式设置为IE5
4. IE=Edge：始终以最新的文档模式来渲染页面，忽略文档类型声明。比如IE10就会用IE10标准模式，IE9就会用IE9标准模式。


而为什么会有这三种模式，实际上是历史遗留问题。在很久以前的网络上，页面通常有两种版本：为网景（Netscape）的 Navigator准备的版本以及为微软（Microsoft）的 Internet Explorer准备的版本。当 W3C 创立网络标准后，为了不破坏当时既有的网站，浏览器不能直接起用这些标准。因此，浏览器采用了两种模式，用以把能符合新规范的网站和老旧网站区分开。  
在怪异模式下，排版会模拟 Navigator 4 与 Internet Explorer 5 的非标准行为。为了支持在网络标准被广泛采用前，就已经建好的网站，这么做是必要的。在标准模式下，行为即（但愿如此）由 HTML 与 CSS 的规范描述的行为。在接近标准模式下，只有少数的怪异行为被实现。  

如果想查看具体有哪些区别 可以看  
https://developer.mozilla.org/en-US/docs/Mozilla/Mozilla_quirks_mode_behavior  
和  
https://developer.mozilla.org/en-US/docs/Gecko's_Almost_Standards_Mode  