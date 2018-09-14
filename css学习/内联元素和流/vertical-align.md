# 起作用的前提条件
 * 只能应用于内联元素以及 display 值为 table-cell 的元素。
 * vertical-align 属性只能作用在 display 计算值为 inline、inline-
   block，inline-table 或 table-cell 的元素上。因此，默认情况下，span、strong、
   em等内联元素，img、button、input等替换元素，非 HTML 规范的自定义标签
   元素，以及<td>单元格，都是支持 vertical-align 属性的，其他块级元素则不支持。
 * 浮动和绝对定位会让元素块状化，从而让内联元素的vertical-align不生效
 
 # 百分比
 * vertical-align 的百分比值是相对于 line-height 计算的
 * 且是以line-height的基线为基础，vertical-align:0%和vertical-align：baseline效果一样
 
 # vertical-align：inline-block和baseline
 * vertical-align 属性的默认值 baseline 在文本之类的内联元素那里就是字符 x 的下
   边缘，对于替换元素则是替换元素的下边缘。但是，如果是 inline-block 元素则规则要
   复杂了：一个 inline-block 元素，如果里面就是没有图文内容，或者 overflow 不是 visible，
   则该元素的基线就是其 margin 底边缘；否则其基线就是元素里面最后一行内的图文的基线。
   见demo ：inline-block元素的vertical-align.html
   
# vertical-align:middle实现垂直居中
* 内联元素：元素的垂直中心点和行框盒子基线往上 1/2 x-height 处对齐。vertical-align:middle 定义是元素的中线和字符 x 中心点对齐
* table-cell 元素：单元格填充盒子相对于外面的表格行居中对齐。
   
   