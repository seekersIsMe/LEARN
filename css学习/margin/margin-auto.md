# margin:auto 触发的条件
* margin:auto 计算有一个前提条件，就是 width 或 height 为 auto 时，
元素是具有对应方向的自动填充特性的

* 另外，对于替换元素，如果我们设置 display:block，则 margin:auto 的计算规则同
  样适合。替换元素的大小有自己的一套计算规则，设置其display为block也是无法自动填满父元素，不具备自动填充特性
  但是margin-auto确有效