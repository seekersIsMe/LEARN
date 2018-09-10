## css2.1 面向内容（图文信息）设计的 
# 包裹性
  * 该元素设置了absolute后，该元素就会具有inline-block的特性，
  其他有（不设置高度和宽度）浮动、绝对定位、inline-block 元素或 table 元素
  * inline-block，设置inline-block属性后，如果该元素没有设置宽高或者设置宽度和高度为100%，
    则该元素的大小是由其内容或者子元素的大小所有决定，所撑起来
    见demo3

# 破坏性
  * 该元素设置为absolute后，该元素不会撑起其父元素的大小，见demo1
  
  
  
# 替换元素的特性之一就是尺寸由
  内部元素决定，且无论其 display 属性值是 inline 还是 block