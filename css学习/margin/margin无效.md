* display 计算值 inline 的非替换元素的垂直 margin 是无效的（像span）,
但是对于内联替换元素,垂直 margin 有效，并且没有 margin 合并的问题，
所以图片永远不会发生 margin 合并

* 表格中的<tr>和<td>元素或者设置 display 计算值是 table-cell 或 table-row 的
  元素的margin 都是无效的，但是计算值是table-caption、table 或者inline-table的就没有此问题
  
* 内联特性导致的 margin 无效

* 鞭长莫及导致的 margin 无效，见代码，后续再研究，float和overflow有关 
````
<div class="box">
<img src="mm1.jpg">
<p>内容</p>
</div>
.box > img {
float: left;
width: 256px;
}
.box > p {
overflow: hidden;
margin-left: 200px;
}
margin-left:200px 是无效的
````