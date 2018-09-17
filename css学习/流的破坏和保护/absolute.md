# 当 absolute 和 float 同时存在的时候，float属性是无任何效果的
# 块状化、包裹性、破坏性
# 绝对定位元素的宽度是相对于第一个position 不为 static 的祖先元素计算的
# 无依赖绝对定位 见demo无依赖绝对定位absolute.html
* 如果是block的dom和inline的dom，则会换行，如果是inline和inline的就在同一行，总之凡是有block的dom就会换行
* 这里的inline和inline的dom情况，感觉有点和其块状化特性有些冲突，
其实和没有应用 position:absolute 的时候一样，一个换行了，一个在同一行，如果设置display为inline的display为block，
还是会换行