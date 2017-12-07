---
title: 在bootstrap中使用select
date: 2017-11-10 10:41:10
tags: [bootstrap]
categories: [coding]
---
### 记录一下 bootstrap 中 select 的几种方式
#### 1. 在 boostrap 4 以下的版本中
可以使用插件 bootstrap-select 具体的使用方式 [点击这里](https://silviomoreto.github.io/bootstrap-select/)
#### 2. 在 boostrap 4 版本中
目前 bootstrap-select 还不支持4以上的版本。
为了实现 bootstrap 风格的select有这两种方式：
#####  用 bootstrap 的 dropdown 功能实现
html:
```
<h2>Bootstrap Dropdown as Select</h2>
  <div class="btn-group">
    <a class="btn btn-primary dropdown-toggle" data-toggle="dropdown" href="#">Select a Country <span class="caret"></span></a>
    <ul class="dropdown-menu">
      <li class="dropdown-item"><a href="#">Item I</a></li>
      <li class="dropdown-item"><a href="#">Item II</a></li>
      <li class="dropdown-item"><a href="#">Item III</a></li>
      <li class="dropdown-item"><a href="#">Item IV</a></li>
      <li class="dropdown-item"><a href="#">Item V</a></li>
      <li class="dropdown-item"><a href="#">Other</a></li>
    </ul>
  </div>
```
jQuery:
```
$(".dropdown-menu li a").click(function(){
  var selText = $(this).text();
  $(this).parents('.btn-group').find('.dropdown-toggle').html(selText+' <span class="caret"></span>');
});
```
#####  用 bootstrap 的 .form-control 
 bootstrap 4 中提供了 bootstrap 风格的 select 示例代码：
```
<select class=" form-control ">
	<option>###</option>
	<option>###</option>
</select>
```
