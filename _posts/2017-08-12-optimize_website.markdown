---
layout: post
title:  " 网站优化的建议"
date:   2017-08-12 21:10:00 +0800
categories: Web
---
#### 服务器端
1. **将辅助资源分开存放**

    提到辅助资源实际上说的是图片或者静态script文件等不需要服务器端处理的文件。
    这点不是必需的，但是考虑服务器的稳定性我们确实有很多理由去采取这种措施以防资源拥堵。  
>更多参考阅读：http://yuiblog.com/blog/2007/04/11/performance-research-part-4/  

2. ** 用GZip压缩 **  

    简而言之，当有HTTP请求的时候，就会有内容从服务器端发送到客户端。而压缩这个内容会减少每一个请求需要的内容的发送时间。 

3. ** 减少重定向 **   

    重定向的理由有很多，比如想让用户从一个旧的网页跳到最新版的网页，或者仅仅是将用户引导到正确的网页上。每一次重定向都会创建一个额外的HTTP请求和RTT(round-trip-time)，你重定向的次数越多，用户到达目标网站的速度越慢。

4. ** 减少DNS查询 **
    
    参考Yahoo! Developer Network Blog，DNS需要花费20-120毫秒去将给定的域名转化为相应的IP地址，而在此期间，浏览器什么都做不了。
	所以建议将各个组件划分成至少两个但是不要超过四个域以减少DNS查找，并且允许并行下载。
	

#### 优化资源（CSS, Javascripts,图像）
1. **将多个Javascript文件整合成一个**

    比如将
    ```
    http://www.creatype.nl/javascript/prototype.js
    http://www.creatype.nl/javascript/builder.js
    http://www.creatype.nl/javascript/effects.js
    http://www.creatype.nl/javascript/dragdrop.js
    http://www.creatype.nl/javascript/slider.js  
    ```
    换成
    ```
    http://www.creatype.nl/javascript/prototype.js,builder.js,effects.js,dragdrop.js,slider.js
    ```  
    
2. **压缩文件**

    现在有很多压缩JavaScript文件和CSS文件的工具，可以自行选择喜欢的。

3. **自定义Header里的Expiry/Caching**

    使用自定义的过期头可以在同一个用户第二次访问你的界面的时候跳掉关于静态文件的不必要的HTTP请求。

4. **从其他地方加载资源**

    这点的意思是将你的静态文件放在并非你部署网站的其他服务器上。将会对服务器速度有显著的提升。

>可以以参考雅虎工程师给出的35个最佳实践
Best Practices for Speeding Up Your Web Site  http://developer.yahoo.com/performance/rules.html
还有相应的测试工具Yslow http://developer.yahoo.com/yslow/