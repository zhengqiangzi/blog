---
title: javascript / css 中的小技巧
date: 2017-08-14 16:23:24
tags: javascript
---

### 给文本加链接  ###

```
"baidu".link("http://www.baidu.com")=<a herf="http://www.baidu.com>baidu</a>"
```


### setTimeout执行绑定参数 ###

```

var callback = function(a,b){

	console.log(a + b);  // 'foobar'

}
setTimeout(callback,100,'foo','bar')
```

### 创建长宽比固定的元素 ###
 通过设置父级窗口的padding-bottom可以达到让容器保持一定的长度比的目的，这在响应式页面设计中比较有用，能够保持元素不变形。
 注:当padding-bottom的值为百分比时，其它百分比的参照值为当前元素的宽度 



### 整数的操作 ###


JavaScript中是没有整型概念的，但利用好位操作符可以轻松处理，同时获得效率上的提升。
|0和~~是很好的一个例子，使用这两者可以将浮点转成整型且效率方面要比同类的parseInt,Math.round 要快。在处理像素及动画位移等效果的时候会很有用。
```
var foo = (12.4 / 4.13) | 0;//结果为3
var bar = ~~(12.4 / 4.13);//结果为3
```

``` 顺便说句，!!将一个值方便快速转化为布尔值 !!window===true ```

### 万物皆对象 ###

在JavaScript的世界，万物皆对象。除了null和undefined，其他基本类型数字，字符串和布尔值都有对应有包装对象。对象的一个特征是你可以在它身上直接调用方法。对于数字基本类型，当试图在其身上调用toString方法会失败，但用括号括起来后再调用就不会失败了，内部实现是用相应的包装对象将基本类型转为对象。所以

*** 1.toString()==new Number(1).toString() ***


因此，你的确可以把基本类型数字，字符串，布尔等当对象使用的，只是注意语法要得体。

同时我们注意到，JavaScript中数字是不分浮点和整形的，所有数字其实均是浮点类型，只是把小数点省略了而以，比如你看到的1可以写成1.，这也就是为什么当你试图1.toString()时会报错，所以正确的写法应该是这样：1..toString()，或者如上面所述加上括号，这里括号的作用是纠正JS解析器，不要把1后面的点当成小数点。内部实现如上面所述，是将1.用包装对象转成对象再调用方法。

### console.table ###
Chrome专属，IE绕道的console方法。可以将JavaScript关联数组以表格形式输出到浏览器console，效果很惊赞，界面很美观。

![image](/images/q4.png)