---
title: 写一个简单的babel-plugin
date: 2017-08-14 17:19:10
tags: javascript
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

** 目标 **

```	
function square(n) {
 return n * n;
}

```
上面是一个javascript中的普通函数声明，执行此函数，传入参数据n,返回的是n的平方.出于研究的目的，现在希望返回的是 *** z X z ***

在不知道babel转换的原理之前，我们设想这样的操作应该是这样几种情况   **(至少我只能想到这几种情况):** 

+ 用字符串方式把``n``替换成``z``

+ 用正则方式把 ``n``替换成``z``

###### **** 但是这样的转换复杂，而且不易于后期的维，字符串替换真的准确吗 那就请出babel转换的工具吧 **** ######

### [babylon](https://www.npmjs.com/package/babylon "Babylon 是 Babel 的解析器") ###

Babylon 是 Babel 的解析器,它主要是把 javascript代码转换成一个ast语法树,上面的一个函数经过传换后，就变成了一个tree,[详情查看](http://astexplorer.net/#/Z1exs6BWMq)



### [babel-traverse](https://www.npmjs.com/package/babel-traverse "Babel Traverse（遍历）模块维护了整棵树的状态，并且负责替换、移除和添加节点。") ###

Babel Traverse（遍历）模块维护了整棵树的状态，并且负责替换、移除和添加节点。


### [babel-types](https://www.npmjs.com/package/babel-types )

Babel Types模块是一个用于 AST 节点的 Lodash 式工具库（译注：Lodash 是一个 JavaScript 函数工具库，
提供了基于函数式编程风格的众多工具函数）， 它包含了构造、验证以及变换 AST 节点的方法


### [babel-generator](https://www.npmjs.com/package/babel-generator)

Babel Generator模块是 Babel 的代码生成器，它读取AST并将其转换为代码和源码映射（sourcemaps）。


通上面一些工具和官方提供的文档，做了一次简单的转换


``` 
import * as babylon from "babylon";
import * as t from 'babel-types';
import traverse from "babel-traverse";
import generate from 'babel-generator'
import template from "babel-template";
const code = `function square(n) {
  return n * n;
}`;
const ast = babylon.parse(code);
traverse(ast, {
  enter(path) {
    if (t.isIdentifier(path.node, { name: "n" })) {
        path.node.name = "x";
    }
  }
});
var r_code = generate( ast ) 

console.log(r_code) //后就是转换成的代码了.
```