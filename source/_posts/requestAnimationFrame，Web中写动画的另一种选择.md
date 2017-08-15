---
title: requestAnimationFrame，Web中写动画的另一种选择
date: 2017-08-14 13:56:10
tags: css
---
> ** requestAnimationFrame存在的必要性 **

HTML5/CSS3时代，我们要在web里做动画选择其实已经很多了:
你可以用CSS3的animattion+keyframes;
你也可以用css3的transition;
你还可以用通过在canvas上作图来实现动画，也可以借助jQuery动画相关的API方便地实现;
当然最原始的你还可以使用window.setTimout()或者window.setInterval()通过不断更新元素的状态位置等来实现动画，前提是画面的更新频率要达到每秒60次才能让肉眼看到流畅的动画效果。
现在又多了一种实现动画的方案，那就是还在草案当中的 ** window.requestAnimationFrame() ** 方法。

 ### 初识requestAnimationFrame ###

 ---

 #### 基本语法 ####

 可以直接调用，也可以通过window来调用，接收一个函数作为回调，返回一个ID值，通过把这个ID值传给window.cancelAnimationFrame()可以取消该次动画。

 ** 示例 **

```
 requestAnimationFrame(callback)//callback为回调函数 

<div id="test" style="width:1px;height:17px;background:#0f0;">0%</div><input type="button" value="Run" id="run"/>

window.requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame || window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;var start = null;var ele = document.getElementById("test");var progress = 0;function step(timestamp) {
    progress += 1;
    ele.style.width = progress + "%";
    ele.innerHTML=progress + "%";    if (progress < 100) {
        requestAnimationFrame(step);
    }
}
requestAnimationFrame(step);

document.getElementById("run").addEventListener("click", function() {
    ele.style.width = "1px";
    progress = 0;
    requestAnimationFrame(step);
}, false);



	
```