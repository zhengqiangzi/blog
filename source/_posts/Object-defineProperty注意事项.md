---
title: Object.defineProperty注意事项
date: 2017-08-14 17:09:35
tags: javascript
---
 Object.defineProperty() 方法设置属性时，属性不能同时声明访问器属性（ set 和 get ）和 writable 或者 value 属性。 意思就是，某个属性设置了 writable或者 value 属性，那么这个属性就不能声明 get 和 set 了，反之亦然。

因为 Object.defineProperty() 在声明一个属性时，不允许同一个属性出现两种以上存取访问控制。

```
	var o = {},
    myName = 'erik';
	Object.defineProperty(o, 'name', {
	    value: myName,
	    set: function(name) {
	        myName = name;
	    },
	    get: function() {
	        return myName;
	    }
	});
```
上面的代码看起来貌似是没有什么问题，但是真正执行时会报错，报错如下，

```
TypeError: Invalid property.  A property cannot both have accessors and be writable or have a value, #<Object>

```

因为这里的 name 属性同时声明了 value 特性和 set 及 get 特性，这两者提供了两种对 name 属性的读写控制。这里如果不声明 value 特性，而是声明 writable 特性，结果也是一样的，同样会报错。

