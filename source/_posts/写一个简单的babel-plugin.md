---
title: 写一个简单的babel-plugin
date: 2017-08-14 17:19:10
tags:
---
> 在nodeJS强大的威力下，javascript能做的事越来越多，在之前的项目中有用到es6、es7的语法，由于有babel的支持，所以兼容性的问题不存在了。
之前一直用babel的plugin来转换语法，比如箭头函数

```
	let a=_=> _+1

```

象这种语法结构 ，如果不解析的话，稍微老一点的浏览器会不识别此类方法，然后抛出一个错误.

babel转换器依靠nodeJS作用运行环境，把上述代码在底层转换成
```
var a=function( _ ){
	
	return _ + 1
}

```
这样就是老式的一个普通 函数，浏览器运行起来豪无压力。

*** 那babel到底是怎样做的了？ ***


[关于babel的plugin详情，请点击 plugin-handbook ](https://github.com/thejameskyle/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md)


我这里只描述我自已对babel 自定义plugin的理解：