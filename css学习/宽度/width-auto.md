* 默认情况下中文是随便断的，英文单词不能断，除非设置（white-space:nowrap）

# 充分利用可用空间。
* 比方说，<div>、<p>这些元素的宽度默认是 100%于父级容器的。这种充分利用可用空间的行为还有个专有名字，叫作 fill-available，大家了解即可。
# 收缩与包裹。
 * 典型代表就是浮动、绝对定位、inline-block 元素或 table 元素，英文称为 shrink-to-fit，直译为“收缩到合适”，有那么点儿意思，但不够形象，我一直把这种现
   象称为“包裹性”。CSS3 中的 fit-content 指的就是这种宽度表现。
# 收缩到最小。
 * 这个最容易出现在 table-layout 为 auto 的表格中，想必有经验的人一定见过图 3-4 所示的这样一柱擎天的盛况吧！
 眼见为实，有兴趣的读者可以手动输入http://demo.cssworld.cn/3/2-1.php 或者扫下面的二维码。
 图 3-4 单元格中的一柱擎天效果当每一列空间都不够的时候，文字能断就断，但中文是随便断的，英文单词不能断。于是，
 第一列被无情地每个字都断掉，形成一柱擎天。这种行为在规范中被描述为“preferred minimum
 width”或者“minimum content width”。后来还有了一个更加好听的名字 min-content。
# 超出容器限制。
* 除非有明确的 width 相关设置，否则上面 3 种情况尺寸都不会主动超过父级容器宽度的，但是存在一些特殊情况。例如，内容很长的连续的英文和数字，或者内联
 元素被设置了 white-space:nowrap，