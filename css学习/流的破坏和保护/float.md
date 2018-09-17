# 特性
* 包裹性；当width为auto
* 块状化并格式化上下文；display变为block或者table,只有设置为inline-table的dom会被转化成table，其他类型会被转成block
* 破坏文档流；
* 没有任何 margin 合并；


# clear
* clear 属性只有块级元素才有效的，而::after 等伪元素默认都是内联水平，这就是借
  助伪元素清除浮动影响时需要设置 display 属性值的原因。