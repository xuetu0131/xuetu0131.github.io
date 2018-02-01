---
title: bootstrap 4 collapse list-group
date: 2018-02-01 15:49:14
tags: [bootstrap]
categories: [coding]
---
###记录一下bootstrap 4中如何产生可以下拉的list group
在使用list group时想要做一个可以下拉的sidebar但是如果只是简单的使用collapse产生的下拉内容会重新生成一个下拉表格如下
![图例1](/assets/img/collapse1.jpg)
这样的话collapse的内容会形成两个圆角，不美观。
但是自己又懒的写css所以想了个直接用bootstrap的解决方法：
直接上代码
```
	<div class="list-group">
		<a class="list-group-item list-group-item-action" id="" href="#" data-toggle="collapse" data-target="#collapseOne">items</a>
		<div class="collapse show " id="collapseOne">
			<a class="list-group-item list-group-item-action d-none" id="" href="#"></a>
			<a class="list-group-item list-group-item-action" id="" href="#">item1</a>
			<a class="list-group-item list-group-item-action" id="" href="#">item2</a>
			<a class="list-group-item list-group-item-action" id="" href="#">item3</a>
			<a class="list-group-item list-group-item-action" id="" href="#">item4</a>
			<a class="list-group-item list-group-item-action d-none" id="" href="#"></a>
		</div>
		<a class="list-group-item list-group-item-action" id="" href="#">items</a>
		<a class="list-group-item list-group-item-action" id="" href="#">items</a>
	</div>
```
结果：
![图例2](/assets/img/collapse2.jpg)

这个方法在collapse内容的两端加一个空的`<a>`标记，再将这两个空的标记利用`d-none`隐藏就可以达到原生list group的效果。**但是这样的话不能把最后一个list item添加collpse**。