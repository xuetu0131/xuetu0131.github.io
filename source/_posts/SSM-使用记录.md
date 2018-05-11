---
title: SSM 使用记录
date: 2018-02-02 15:03:57
tags: [SSM]
categories: [coding]
---
###记录在使用SSM(Spring,SpringMVC,Mybatis)中遇到的问题
#### 1.基于注解式
在接受请求时可能带有大量的参数，理论上来说controller不处理业务，所以应当将参数都传入service中去处理，但是这样会使你每个方法相当臃肿，并且难以阅读（虽然本来就只有我自己看得懂）。在这个问题上纠结了好久，回顾SpringMVC文档时，突然发现SpringMVC对参数是有自动注入的功能的。所以就尝试着使用注入的方式将参数封装对象。
直接在方法的参数中用你想要的对象，SpringMVC会自动进行属性的注入，并且会对相应的简单数据类型进行类型转换。
```
	public void yourMethod(Object yourObject){
		//--------------
	}
```
如果有参数不能直接放入`yourObject`中可以在添加`@RequestParam`注解获取其他参数。有时参数不是必须的可以使用reqired属性设置为false则SpringMVC会将null值设给接受参数。
**因为会赋值为null，所以在接受参数时尽量使用包装类**
```
	public void yourMethod(Object yourObject,@RequstParam(value="arg0",required=false)Integer arg0){
		//--------------
	}
```
在使用过程中难免会遇到一些复杂对象，这时就需要自己对参数进行数据类型转换或对象封装。
单个controller可以直接使用`@initBinder`
多个controller中需要单独写`@controllerAdvice`类使得对所有的请求在需要转换成你的对象时自动调用
```
@ControllerAdivice
public class MyControllerAdivice{
	@initBinder
	public void initBinder(WebDataBinder binder){
		binder.registerCustomEditor(yourObject.class, new TimeStampPropertyEditor() );
	}
}
```
其中第二个参数是我自己写的将`String`转换为`Timpstamp`类的`PropertyRditor`，也可以用`formattor`（目前还没看懂怎么搞，所以先用自己写的）
自己写需要继承PropertyEditorSupport类,具体代码如下：
```
public class TimeStampPropertyEditor extends PropertyEditorSupport {
	private Timestamp timestamp;

	@Override
	public void setAsText(String text) throws IllegalArgumentException {
		// TODO Auto-generated method stub
		SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-mm-dd");
		try {
			timestamp = new Timestamp(simpleDateFormat.parse(text).getTime());
		} catch (ParseException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		setValue(timestamp);
	}
	
}
```
其中`text`是将要传入的String，`setValue`可以是`yourObject`也可以是转换数据类型后的结果,具体可以查看`PropertyEditor`接口的文档介绍。