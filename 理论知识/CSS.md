### 1. transition的属性值和应用

属性的名称 过渡时间 时间曲线 延迟

### 2. rem和em的区别

em相对于父元素，rem相对于根元素

### 3. position的值， relative和absolute分别是相对于谁进行定位的？
relative:相对定位，相对于自己本身在正常文档流中的位置进行定位。
absolute:生成绝对定位，相对于最近一级定位不为static的父元素进行定位。
fixed: 生成绝对定位，相对于浏览器窗口或者frame进行定位。
static:默认值，没有定位，元素出现在正常的文档流中。
sticky:生成粘性定位的元素，容器的位置根据正常文档流计算得出。
### 4.position:absolute和float属性的异同？
共同点：对内联元素设置float和absolute属性，可以让元素脱离文档流，并且可以设置其宽高。
不同点：float仍可占据位置，不会覆盖在另一个BFC区域上，浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止。absolute会覆盖文档流中的其他元素。

### 5.CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？
选择器
> 1.id选择器
  2.类选择器
  3.标签选择器
  4.相邻选择器(h1+p)
  5.自选择器(ul>li)
  6.后代选择器(li a)
  7.通配符选择器(*)
  8.属性选择器(button[disabled="true"])
  9.伪类选择器(a:hover,li:nth-child)表示一种状态
  10.伪元素选择器(li:before)表示文档某个部分
  
优先级  
!important > 行内样式（比重1000） > id（比重100） > class/属性（比重10） > tag / 伪类（比重1）;
伪类和伪元素区别：
1>、伪类：a:hover,li:nth-child；
2>、伪元素：li:before、:after,:first-letter,:first-line,:selecton;

### 6.