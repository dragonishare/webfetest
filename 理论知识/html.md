# html 相关问题

### 1.知道语义化吗？说说你理解的语义化，如果是你，平时会怎么做来保证语义化

像html5的新的标签header，footer,section等就是语义化

一方面，语义化就是让计算机能够快速的读懂内容，高效的处理信息，可以对搜索引擎更友好。

另一方面，便于与他人的协作，他人通过读代码就可以理解你网页标签的意义。

### 2.说说content-box和border-box，为什么看起来content-box更合理，但是还是经常使用border-box

content-box 是W3C的标准盒模型 元素宽度=内容宽度+padding+border

border-box 是ie的怪异盒模型  他的元素宽度等于内容宽度  内容宽度包含了padding和border

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

### 7. 


