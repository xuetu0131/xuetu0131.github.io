---
title: border-img 制作QQ气泡
date: 2018-05-11 16:28:31
tags: [css]
categories: [coding]
---
### 使用border-image制作类似QQ气泡的效果
刚刚学习了Node和Vue想做一个聊天室，在制作气泡效果的时候发现出现了一些问题。如果使用一般的网上的方法都会有一些限制。     
1. css不好调，需要各种对齐；
2. 当文字段落很长时，有需要进一步的设置，甚至需要javasript操作。        
最后发现了使用boder-image的这种方法。
首先气泡![图例](/assets/img/bubble.png)
想要让这个图片作为边框将文字包裹起来需要这样做。
在设置border-image之前必须先设置border属性：
```
border: 15px solid transparent;
```
之后再设置border-image
```
//我用的是chrome使用第二个
/* border-image: url("resource/Group 3.png") 40 15 15 30 10px stretch; */
//参数 1.地址 2.图片的切割 3.边界处理方法
-webkit-border-image: url("resource/Group 3.png") 40% 30% 30% 55% stretch;
```
1. 图片存放位置
2. 图片的切割       
    不带单位或百分比，不能用px;
    ![分割参数](/assets/img/bubble-slice.png)
3. 有以下以几种不同的方法
    图片样例:[w3school](http://www.w3school.com.cn/tiy/t.asp?f=css3_border-image)
     - repeat 重复
     - round 在重复的基础上，保证不会出现半张图片的情况
     - sketch 拉伸

    可以同时接受两个表示左右和上下不同的处理方法。