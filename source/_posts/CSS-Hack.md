---
title: CSS Hack
tags: css
date: 2017-08-14 15:27:00
---

1. css样式选择器中存在两个名称相同的属性，浏览器一般会以最后面的属性为准。
** IE加上一个下划线“_”，IE 6 照样可以识别该属性，而且只有IE 6可以识别。**

2. 特定的css属性值后缀“\9”，从而做到只有IE8及以下浏览器能够识别该属性

3. IE 7也支持在选择器前添加*+html和*:first-child+html ，让当前选择器成为*+html的后辈选择器，只有IE 7可以识别此类样式选择器

4. 只有IE8支持嵌套如下@media类型查询语句：@media \0screen

5. background-color:red\0;IE8和IE9都支持；

6. background-color:blue\9\0; 仅IE9支持；