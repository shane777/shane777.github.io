---
layout: post
title:  " Vue.extend()和Vue.component()的区别"
date:   2017-08-02 23:00:00 +0800
categories: Vue
---
在Vue.js中，Vue本身是一个constructor。  
Vue.extend() 是一个继承于方法的 class，参数是一个包含组件选项的对象。它的目的是创建一个Vue的子类并且返回相应的 constructor。  
而Vue.component()实际上是一个类似于Vue.directive() 和 Vue.filter()的注册方法，它的目的是给指定的一个constructor一个String类型的ID，
之后Vue.js可以把它用作模板，实际上当你直接传递选项给Vue.component()的时候，它会在背后调用Vue.extend()。

Vue.js支持两种不同的API模型：一种是基于类的，命令式的，Backbone 类型的API；另一种是基于标记语言的，声明式的，Web组件类型的API。   
如果还是困惑的话，可以想象你是怎么创建通过new Image()或者 <img>标签创建 image元素的就知道了。  
 这两种方法都对指定的类型很有用，Vue.js提供这两者只是为了更好的灵活性。
