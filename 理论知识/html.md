# html 相关问题

### 1.知道语义化吗？说说你理解的语义化，如果是你，平时会怎么做来保证语义化

像html5的新的标签header，footer,section等就是语义化

一方面，语义化就是让计算机能够快速的读懂内容，高效的处理信息，可以对搜索引擎更友好。

另一方面，便于与他人的协作，他人通过读代码就可以理解你网页标签的意义。

### 2.说说content-box和border-box，为什么看起来content-box更合理，但是还是经常使用border-box

content-box 是W3C的标准盒模型 元素宽度=内容宽度(width)+padding+border

border-box 是ie的怪异盒模型  他的元素宽度等于内容宽度(width)  内容宽度包含了padding和border

比如有时候在元素基础上添加内距padding或border会将布局撑破 但是使用border-box就可以轻松完成

### 3. 介绍一下HTML5的新特性

* 新的DOCTYPE声明  `<!DOCTYPE html>`
* 完全支持css3
* video和audio 
* 本地存储 
* 语义化标签
* canvas 
* 新事件 如ondrag onresize

### 4. 实现两栏布局有哪些方法
* 1.float，左边浮动，右边margin-left
* 2.float，左边浮动，右边overflow:hidden
> 我利用的是创建一个新的BFC（块级格式化上下文）来防止文字环绕的原理来实现的。BFC就是一个相对独立的布局环境，它内部元素的布局不受外面布局的影响。它可以通过以下任何一种方式来创建： 
float 的值不为 none 
position 的值不为 static 或者 relative 
display 的值为 table-cell , table-caption , inline-block , flex , 或者 inline-flex 中的其中一个 
overflow 的值不为 visible
* 3.position，左边固定定位，右边margin-left
* 4.position，左边固定定位，父元素padding-left
* 5.flex，左边flex:none不放大也不缩小，父元素设置flex，右边自适应

### 5. offsetHeight, scrollHeight, clientHeight分别代表什么

clientHeight：包括内容可见部分的高度，可见的padding；不包括border，水平方向的scrollbar，margin。

offsetHeight：包括内容可见部分的高度，border，可见的padding，水平方向的scrollbar（如果存在）；不包括margin。

scrollHeight：包括内容的高度（可见与不可见），padding（可见与不可见）；不包括border，margin。

### 6. 垂直居中

单行行内元素 1.可以设置padding-top,padding-bottom 2.将height和line-height设为相等

多行行内元素 1.可以将元素转为table样式，再设置vertical-align：middle; 2.使用flex布局

块级元素

已知高度绝对定位负边距

未知高度transform: translateY(-50%);

flex布局 
display: flex;
justify-content: center;
align-items: center;

### 7. 清除浮动
两种原理：

1、利用clear属性进行清理

具体的实现原理是通过引入清除区域，这个相当于加了一块看不见的框把定义clear属性的元素向下挤
父容器结尾插入空标签`<div style="clear: both;"></div>`

利用CSS伪元素：
```css
.clearfix:after {
  content: ".";
  height: 0;
  visibility: hidden;
  display: block;
  clear: both;
}
```
通过将这个类添加到父容器当中，会在父容器的末尾增加了一个高度为0、具有清除属性的、不可见的块级元素。
2、将父容器形成BFC

BFC能清理浮动主要运用的是它的布局规则：

内部的Box会在垂直方向，一个接一个地放置。
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
BFC的区域不会与float box重叠。
BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
计算BFC的高度时，浮动元素也参与计算
浮动清理利用的主要是第六条规则，只要将父容器触发为BFC，就可以实现包含的效果。

那么触发BFC有哪几种方法？

* 根元素
* float属性不为none
* position为absolute或fixed
* display为inline-block, table-cell, table-caption, flex, inline-* flex
* overflow不为visible

### 8.
