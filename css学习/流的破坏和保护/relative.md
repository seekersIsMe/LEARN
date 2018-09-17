# 一是相对自身，定位的参考点是相对自己的，但是left等百分比值是相对包含块的
# 二是无侵入，不会影响周围的元素定位
# 最小化影响原则
* 尽量不使用 relative，如果想定位某些元素，看看能否使用“无依赖的绝对定位”；
* 如果场景受限，一定要使用 relative，则该 relative 务必最小化。例如：
```
<div>
<div style="position:relative;">
<img src="icon.png" style="position:absolute;top:0;right:0;">
</div>
<p>内容 1</p>
<p>内容 2</p>
<p>内容 3</p>
<p>内容 4</p>
...
</div>
```


而不是如下：如果页面复杂了就可能有层级的问题
````
<div style="position:relative;">
<img src="icon.png" style=
"position:absolute;top:0;right:0;">
<p>内容 1</p>
<p>内容 2</p>
<p>内容 3</p>
<p>内容 4</p>
...
</div>
````