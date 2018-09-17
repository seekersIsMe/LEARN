# overflow 剪裁界线是border box而不是padding box
# padding-bottom兼容问题
* Chrome padding-bottom 也算在滚动尺寸之内，如果设置padding-bottom为10px，则滚动到底部会发现，底部有一条10px的空白
* IE和Firefox 则不算在其中，且没有白条
* 我们在实际项目开发的时候，要尽量避免滚动容器设置 padding-bottom 值

> 除了样式表现不一致外，还会导致 scrollHeight 值不一样 

# overflow-x 和 overflow-y 的属性值都是 visible，否则 visible 会当成 auto 来
  解析。换句话说，永远不可能实现一个方向溢出剪裁或滚动，另一方向内容溢出显示的效果。
  
  * visible：默认值。
  * hidden：剪裁。
  * scroll：滚动条区域一直在。
  * auto：不足以滚动时没有滚动条，可以滚动时滚动条出现。
  
# 根元素html和文本域textarea默认产生滚动条


