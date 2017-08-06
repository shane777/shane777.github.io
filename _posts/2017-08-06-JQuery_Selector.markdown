---
layout: post
title:  " Vue.extend()和Vue.component()的区别"
date:   2017-08-06 14:00:00 +0800
categories: JQuery
---
想做一份JQuery选择器的列表，po到这里可以时刻复习。就从网上找了一篇比较全的，自己进行了修订。  


```
$("#myELement")    选择id值等于myElement的元素，id值不能重复在文档中只能有一个id值是myElement所以得到的是唯一的元素  
$("div")           选择所有的div标签元素，返回div元素数组  
$(".myClass")      选择使用myClass类的css的所有元素  
$("*")             选择文档中的所有的元素，可以运用多种的选择方式进行联合选择：例如$("#myELement,div,.myclass")  
```  

层叠选择器： 
```  
$("form input")         选择所有的form元素中包含的input元素  
$("#main > *")          选择id值为main的所有的子元素  
$("label + input")     选择所有的label元素的下一个input元素节点，经测试选择器返回的是label标签后面直接跟一个input标签的所有input
标签元素  相当于$("label").next("input")  
$("#prev ~ div")       同胞选择器，该选择器返回的为id为prev的标签元素的后面的属于同一个父元素的div标签 相当于 $("prev").nextall("div")。 
与前后位置无关，只要同节点就能匹配。  
```  

基本过滤选择器：   
```
$("tr:first")               选择所有tr元素的第一个  
$("tr:last")                选择所有tr元素的最后一个  
$("input:not(:checked) + span")   过滤掉：checked的选择器的所有的input元素  
$("tr:even")               选择所有的tr元素的第0，2，4... ...个元素（注意：因为所选择的多个元素时为数组，所以序号是从0开始  
$("tr:odd")                选择所有的tr元素的第1，3，5... ...个元素  
$("td:eq(2)")             选择所有的td元素中第三个td元素（index 从 0 开始）  
$("td:gt(4)")             选择td元素中index大于4的所有td元素  
$("td:lt(4)")              选择td元素中index小于4的所有的td元素  
$(":header")             选择标题元素  
$("div:animated")    选择正在执行的 动画元素  
$(":focus")                 获得焦点的元素  
```

内容过滤选择器： 
```  
$("div:contains('John')") 选择所有div中含有John文本的元素 
$("td:empty")           选择所有的为空（也不包括文本节点）的td元素的数组   
$("div:has(selector)")        选择所有含有相应选择器标签的div元素  
$("td:parent")          选择所有的以td为父节点的元素数组  
```


可视化过滤选择器：
```  
$("div:hidden")        选择所有的被hidden的div元素  
$("div:visible")        选择所有的可视化的div元素  
```

属性过滤选择器：  
```  
$("div[id]")              选择所有含有id属性的div元素  
$("input[name='newsletter']")    选择所有的name属性等于'newsletter'的input元素  
$("input[name!='newsletter']") 选择所有的name属性不等于'newsletter'的input元素  
$("input[name^='news']")         选择所有的name属性以'news'开头的input元素  
$("input[name$='news']")         选择所有的name属性以'news'结尾的input元素  
$("input[name～='news']")          选择用空格分开的name属性中包含'news'的input元素  
$("input[id][name$='man']")    可以使用多个属性进行联合选择，该选择器是得到所有的含有id属性并且那么属性以man结尾的元素  
```

子元素过滤选择器：  
```
$("ul li:nth-child(2)"),$("ul li:nth-child(odd)"),$("ul li:nth-child(3n + 1)") nth-child的index从1起算 其也eq()的区别可以查看
http://www.jianshu.com/p/9f0b4627b456
$("p:first-child")          选择所有是其父元素的首个子元素的p节点所组成的数组  
$("p:last-child")           选择所有是其父元素的最后一个子元素的p 节点所组成的数组  
$("p:only-child")       选择所有是其父元素的唯一一个子元素的p节点所组成的数组  
```

表单元素选择器：  
```
$(":input")                  选择所有的表单输入元素，包括input, textarea, select 和 button    
$(":text")                     选择所有的text input元素  
$(":password")           选择所有的password input元素  
$(":radio")                   选择所有的radio input元素  
$(":checkbox")            选择所有的checkbox input元素  
$(":submit")               选择所有的submit input元素  
$(":image")                 选择所有的image input元素  
$(":reset")                   选择所有的reset input元素  
$(":button")                选择所有的button input元素  
$(":file")                     选择所有的file input元素  
$(":hidden")               选择所有类型为hidden的input元素或表单的隐藏域  
```

表单元素过滤选择器：  
```
$(":enabled")             选择所有的可操作的表单元素  
$(":disabled")            选择所有的不可操作的表单元素  
$(":checked")            选择所有的被checked的表单元素  
$("select option:selected") 选择所有的select 的子元素中被selected的元素  
```
参考： http://www.cnblogs.com/onlys/articles/jQuery.html