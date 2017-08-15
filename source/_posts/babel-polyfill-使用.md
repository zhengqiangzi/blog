---
title: babel-polyfill 使用
date: 2017-08-14 13:36:35
tags: javascript
---

> 在babel出现之前。如果开发者想使用javascript最新的特点的api，非常困难。究其原因，兼容性太差。为了能使用最新的api，要么自己模拟一下，要么网上down一下，
痛苦。。。。
 这段痛苦的岁月，相信大部分开发都都有过体验，产品经理总是会和你说，“你看这里报错了。。那里报错了。。。。”
心中一群草泥玛呼萧而过。

至到它的出现。**Babel**
相信使用过他的同学，应该知道这是一个多么牛B的转换器。

今天和大一起讨论一下 Babel-polyfill这个包的作用

**官网是这么说的，那些需要修改内置api才能达成的功能，譬如：扩展String.prototype，给上面增加includes方法，就属于修改内置API的范畴。这类操作就
由polyfill提供。**

我理解上面的意思是说。babel-polyfill只对api进行一个修补,说太多没有什么直观的感觉，来点例子吧

> 浏览器环境:

ES6中在String.prototype上面定义了一个新的方法 padLeft的代码未使用 poly-fill时

![image](/images/q1.png)


> 在代码中作用poly-fill时

![image](/images/q2.png)

**此时证明,poly-fill已经修补了padLeft这个在String.prototype上面的方法**


那babel-polyfill到底修改了多少个api了，想找到这个答案的，那就打开babel-polyfill的源码吧

![image](/images/q3.png)

相信看到这里，应该明白了，那些方法是被修补了吧！


### 思考：###

引用 babel-polyfill 解决了es5的api文题，babel-polyfill是通过全局覆盖的形式来处理问题的，那如果我做的项目一个库或是一个工具时也引用了babel-polyfill，那使用者在引用这个库或工具时，是不是要崩溃（只是引用一个工具而已，你把别人的全局环境污染了，而且你还送给别人一堆可能没有用的代码。。。。）



### 解决方法 ###

 #### babel-runtime / babel-plugin-transform-runtime ####
 babel-runtime 可以自动识别需要修改的语法，但不是全部，象 Object.assign(),String.prototype.includes方法都不会修复，象Promise,Symbol等会替换修复，这个时候 你需要在你的工具或库文件中给使用者指出那些polyfill需要用户提供.