font-size:14px
* 数值 
    line-height:1.5 则最终结果行高大小为1.5*14=21px

* 百分比 
    line-height:150%
    结果也是21px

* 长度值
   * line-height:21px;
   * line-height:1.5em;结果为21px

# 三者不同点
  * 百分比值或者长度值作为属性值，那么所有的子元素继承的是最终的计算值（继承21px）
  * 数值则子元素继承其属性值