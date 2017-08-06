---
layout: post
title:  " Vue.extend()和Vue.component()的区别"
date:   2017-08-06 14:00:00 +0800
categories: JQuery
---
首先是各个书上都有的概念上的区别：  
1、nth-child(N)：下标从1开始；eq(N)：下标从0开始       
2、nth-child(N)：选择多个元素；eq(N)：选择一个元素  
3、nth-child(N)：在一个文档树种中，选择各层排行第N的所有元素。eq(N)：在一个文档树种中，前序排列后，选择第N个元素  

具体事例   
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript"> 
 
$(document).ready(function(){
    $("p:eq(1)").css("background-color","#B2E0FF");
    $("p:nth-child(1)").css("background-color","#ff0000");
});
 
</script>    
</head>
<body>
  <p>第一个段落。</p>
  <p>第二个段落。</p>
  <p>第三个段落。</p>
  <p>第四个段落。</p>
  <div> -------------< div >----------------------</div>
  <div>
    <p>div下的第一个p</p>
    <p>div下的第二个p</p>
</div>
<body>
```

![screenshot1]({{site.url}}/assets/17post/170806.png)

可以看到nth-child选择了所有在第一位的p元素，eq则选择了全局DOM树中第一个满足条件的p元素