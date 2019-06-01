# CSS 总结

## 块级元素的特点

- 总是从新行开始
- 高度，行高，外边距和内边距都可以控制
- 宽度默认是容器的100%
- 可以容纳内联元素的其他块元素

## 行内元素的特点

行内元素不占有独立的区域，仅仅靠自身的字体的大小和图像尺寸来支持结构，一般不可以设置宽度、高度、对齐等属性，常用于控制页面中文本的样式。

常见的行内元素有：

- `<a></a>`
- `<strong></strong>`
- `<b></b>`
- `<em></em>`
- `<span></span>`

等等


- 和相邻行内元素在一行上
- 宽高无效，但水平方向的`padding` 和 `margin` 可以设置，垂直方向的无效
- 默认宽度就是它本身内容的宽度
- 行内元素只能容纳文本或其他行内元素（`a` 特殊） 

注意：

1. 只有文字才能组成段落，因此 `<p></p>` 里面不能放块级元素，同理还有这些标签`h1`,`h2`,`h3`,`h4`,`h5`,`h6`，他们都是文字类块级元素，里面不能放其他块级元素。

2. 链接里面不能再放链接

## 行内块元素的特点

在行内元素中有几个特殊的标签`img`，`input`,`td`，可以为他们设置宽高和对齐属性。

- 和相邻行内元素（行内块）在一行上，但是之间有空白间隙
- 默认宽度就是它本身内容的宽度
- 宽度、高度、内外边距都可以设置


## 选择器

![选择器](https://github.com/yjn2015/CSS-content/blob/master/img/select.png)

1. 属性选择器


选择器           | 含义                            | 
--------------- |---------------------------------|
 E[attr]        | 存在attr属性即可                 | 
 E[attr=val]    | 属性值完全等于val                | 
 E[attr*=val]   | 属性值里包含val字符串并且在任意位置| 
 E[attr^=val]   | 属性值里包含val字符并且在开始位置  |
 E[attr$=val]   | 属性值里包含val字符并且在结束位置  |


 2. 伪元素选择器

 选择器          | 含义                            | 
--------------- |---------------------------------|
 E:first-letter | 文本的第一个单词或字              | 
 E:first-line   | 文本第一行                       | 
 E:selected     | 可改变选中的文本                  | 

 注意：

 伪类选择器和伪元素选择器的区别：

 1. `:first-child` 伪类选择器，仅有一个冒号的就是伪类选择器
 2. `::first-letter` 伪元素选择器，有两个冒号的话就是伪元素选择器


 3. `E::before` 和 `E::after`

 `before` 和 `after` 是在盒子`div` 内部的前面插入内容或者是内部后面插入内容


 ## CSS 三大特性

 1. CSS 层叠性

 所谓层叠性就是多种样式的叠加，假如样式名称相同，最后的样式会覆盖掉前面的样式。
 样式冲突，遵循的原则就是就近原则，那个样式近就执行那个样式。

 2. CSS 继承性

 `CSS` 继承性是指书写`CSS` 样式表时，子标签会继承父标签的某些样式，如文本颜色和字号，想要设置一个可继承的属性，只需将它应用于父元素即可。

 3. CSS 优先级


 `specificity` 用一个四位字符串来表示，更像四个级别，值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。

继承或者*的贡献值         | 0,0,0,0
-------------------------|----------
 每个元素（标签的贡献值）  | 0,0,0,1 
 每个类，伪类贡献值        | 0,0,1,0
 每个ID贡献值为            | 0,1,0,0
 每个行内样式贡献值         | 1,0,0,0
 每个!important            | 无穷大


 优先级的问题：

 !important > 行内样式 > ID > class > 标签


 注意：

 数位之间没有进制，比如说， 0,0,0,5 + 0,0,0,5 = 0,0,0,10 而不是 0,0,1,0,所以不会存在10个`div` 能赶上一个类选择器的情况。

 总结优先级：

 1. 使用了`!important` 声明的规则
 2. 内嵌在 `html` 元素的`style` 属性里面的声明。
 3. 使用了`ID` 选择器的规则。
 4. 使用了类选择器、属性选择器、伪元素和伪类选择器的规则。
 5. 使用了元素选择器的规则
 6. 只包含一个通用选择器的规则
 7. 同一类选择器遵循就近原则 


## 外边距合并塌陷的问题

1. 什么是外边距合并的概念？

外边距合并指的是，当两个垂直外边距相遇时，它们会形成一个外边距。

合并后的外边距的高度等于两个发生合并的外边距的高度中的较大着。

例子：

当一个元素出现在另一个元素上面时，第一个元素的下外边距于第二个元素的上外边距会发生合并。请看下图：

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/margin_collapsing_example_1.gif)


当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分割开），它们的上和/或下外边距也会发生合并。请看下图：

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/margin_collapsing_example_2.gif)

尽管看上去有些奇怪，但是外边距甚至可以与自身发生合并。

假设有一个空元素，它有外边距，但是没有边框或填充。在这种情况下，上外边距与下外边距就碰到一起，它们会发生合并：

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/css_margin_collapsing_example_3.gif)

如果这个外边距遇到另一个元素的外边距，它还会发生合并：

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/css_margin_collapsing_example_4.gif)

这就是一系列的段落元素占用空间非常小的原因，因为它们的所有外边距都合并到一起，形成了一个小的外边距。

外边距合并初看上去可能有些奇怪，但是实际上，它是有意义的。以由几个段落组成的典型文本页面为例。第一个段落上面的空间等于段落的上外边距。如果没有外边距合并，后续所有段落之间的外边距都将是相邻上外边距和下外边距的和。这意味着段落之间的空间是页面顶部的两倍。如果发生外边距合并，段落之间的上外边距和下外边距就合并在一起，这样各处的距离就一致了。

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/css_margin_collapsing.gif)



```
  <!-- html 代码 -->
  <div class="father">
    <div class="son">

    </div>
  </div>

  <!-- css 代码 -->
  <style>
    .father {
      width: 300px;
      height: 300px;
      background-color: skyblue;
      margin-top: 100px;
      border: 1px solid red; /* 解决外边距合并(塌陷) 问题*/

    }

    .son {
      width: 200px;
      height: 200px;
      background-color: green;
      margin-top: 30px;
    }
  </style>
```

## 定位相关

- `position: static` 作用

一般它用来清除定位的，一个原来有定位的盒子，不想加定位了，就用这句话。

- `position: relative` 

相对定位一般是以自己的左上角为定位点的。

相对定位仍然在标准流中，并且相对定位不脱标。

如果说浮动是让元素一行显示，那么定位的主要价值就是移动位置，让盒子到我们想要的地方去。

- `position: absolute`

若父亲没有定位，那么则以浏览器左上角进行定位（document文档）

绝对定位是根据最近的已经定位（绝对、固定、相对）的父元素 （祖先）定位。就是我们所说的最近原则。


## 定位水平和垂直居中

普通的盒子设置 `margin: 0 auto` 就可以设置一个盒子水平居中，但是对于`absolute` 定位的盒子就无效了。

定位的元素也可以设置水平和垂直居中，有一个算法的概念。

1. 首先`left: 50%`;
2. 然后就是直接的负外边距的一半就可以了。
3. 水平居中就设置`left: 50%` 然后设置盒子本身的宽度的负外边距`margin-left: -xxx;`的一半就可以的了。
4. 垂直居中就设置`top: 50%;` 然后设置`margin-top` 为高度的负的一半就可以的了。

```
.son {
  position: absolute;
  width: 200px;
  hegiht: 200px;
  left: 50%;
  top: 50%;
  margin-left: -100px;
  margin-top: -100px;

}
```

## 固定定位
固定定位有以下两个特点：

1. 固定定位的元素和父亲没有任何的关系，只认浏览器
2. 固定定位完全脱标，不占用位置，不随着滚动条滚动。

## 元素的显示和隐藏

`display: none` 和 `visibility` 的区别：

1. `display: none` 表示隐藏之后，不在保留位置 
2. `visibility: hidden`; 隐藏之后，继续保留位置（停职留薪）

`overflow` 的几个属性：
1. `visible` 不裁剪内容也不添加滚动条
2. `auto` 超出显示滚动条，不超出不显示滚动条
3. `hidden` 超出部分被隐藏
4. `scroll` 不管超没超出内容，总是显示滚动条


## vertical-align 设置行内块元素的垂直居中对齐

例如图片和文字对齐的方式就可以使用这个属性进行设置。

## 去除图片底部缝隙

1. 解决方案

给`img` 添加 `display: block;` 转换为快级元素就不会存在这个问题了。

```
img {
  display: block;
}
```

2. 解决方案2

给`img` `vertical-align: middle | top` 等等，让图片不要和基线对齐。


## 溢出文字隐藏

`word-break` 自动换行

- `normal` 使用浏览器默认的换行规则
- `break-all` 允许在单词内换行
- `keep-all` 只允许在半角空格或连字符处换行。

主要处理英文单词

`white-space` 通常使用于强制一行显示内容

- `normal` 默认处理方式
- `nowrap` 强制在一行内显示所有文本，直到文本结束或者遭遇`br` 标签对象才换行。


`text-overflow` 文字溢出

```
text-overflow: clip | ellipsis
```

是否使用一个省略标记(....) 标示对象内文本的溢出

- `clip` 不显示省略标记，而是简单的裁切
- `ellipsis` 当对象内文本溢出时显示省略标记(....)

> 注意，一定要首先强制一行内显示，再次和`overflow` 属性搭配使用。

## 滑动门核心技术

核心技术就是利用`CSS` 精灵（主要是背景位置）和 盒子`padding` 撑开宽度，以便于能适应不同字数的导航条。

一般的经典布局都是这样的。

```
<li>
  <a href="#">
    <span> 导航栏内容 </span>
  </a>
<li>
```

总结：
  1. `a`设置背景左侧，`padding` 撑开合适宽度。
  2. `span` 设置背景右侧，`padding` 撑开合适宽度剩下由文字继续撑开宽度。
  3. 之所以`a` 包含 `span` 就是因为整个导航都是可以点击的。


具体的代码：

```
  <!-- css 代码 -->
  a {
    display: inline-block;
    height: 33px;
    line-height: 33px;
    margin: 100px;
    padding-left: 15px;
    color: #fff;
    background: url(image/ao.png) no-repeat;
    text-decoration: none;
  }

  a span {
    display: inline-block;
    height: 33px;
    padding-right: 15px;
    background: url(image/ao.png) no-repeat;
  }

  <!-- html 代码 -->
  <a href="#">
    <span> 首页 </span>
  </a>
```

## 伪元素
 
伪元素选择器和伪类选择器的区别：

1. 伪元素选择器，本质上插入一个标签（盒子），代表的有`::before` 和 `::after`
2. 伪元素选择器有两个冒号的。
3. 伪元素默认添加的内容为`inline` 元素
4. 这两个伪元素的`content` 属性，表示伪元素的内容，设置`::before` 和 `::after` 时必须设置其`content` 属性，否则伪元素不起作用。
5. 伪元素是不占位置的。

## 认识过渡效果 `transition`

在 `CSS3` 中，我们可以使用`transition` 实现过渡效果，从一种动效过渡到另一种动效。

并且当前元素只要有“属性”发生变化时即存在两种状态（我们使用A和B进行代指），就可以实现平滑的过渡。

语法格式：

`transition:` 需过渡的属性 花费时间 运动曲线 何时开始；

如果有多组属性变化，还是用逗号隔开。


属性 | 描述 | CSS
---------|----------|---------
 transition | 简写属性，用于在一个属性中设置四个过渡属性 | 3
 transition-property | 规定应用过渡的`CSS` 属性的名称 | 3
 transition-duration | 定义过渡效果花费的时间，默认是0 | 3
 transition-timing-function | 规定过渡效果的时间曲线，默认是 `ease` | 3
 transition-delay | 规定过渡效果何时开始，默认是0. | 3

 
 `transition-timing-function` 运动曲线，属性值可以是：

 - `linear` 线性
 - `ease` 减速
 - `ease-in` 加速
 - `ease-out` 减速
 - `ease-in-out` 先加速后减速

 过渡效果代码示例：

 ```
 div {
   width: 200px;
   height: 100px;
   background-color: skyblue;
   transition: width .6s ease 0s, height .3s ease-in 1s;
 }
 div:hover {
   width: 600px;
   height: 300px;
 }
 ```

 如果需要所有的属性都变化的话，`transition-timing-function` 设置为`all` 即可。

 ## transform 变形

 1. `transform: translate(50%)`

 这里的50%是以自己的宽度为准，而不是以父亲的宽度为准

设置一个元素水平和垂直居中，就可以使用这样的方法：

```
div {
  position: absolate;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
```

2. `scale` 缩放，`scale` 取值默认的值为1，当值设置为0.01 到 0.99 之间的 任何值，作用使一个元素缩小，而任何大于或等于1的值，作用是让元素放大，可以对元素进行旋转，正值为顺时针，负值为逆时针。

案例，鼠标放上去一个过渡的动画效果。

实现的方法需注意两点：

1. `transition: all .3s` 鼠标经过之后的过渡效果
2. `transform: rotate(1.2)` 鼠标经过之后，图片放大的效果

```
<!-- html代码 -->
<div>
  <img src="./img/header.png">
</div>

<!-- css代码 -->
div {
  width: 200px;
  height: 200px;
  overflow: hidden;
}

div img {
   transition: all .3s;
}

div img:hover {
  transform: rotate(1.2);
}
```

这样就可以实现一个鼠标经过之后，图片放大的效果。

## transform-origin

默认开始的旋转的角度为左上角开始选择，例如：

```
div {
  transform-origin: left top;
  // 表示以左上角的顶点为旋转的点
}
```

## transform skew 倾斜

skew为正值，表示的是往左边倾斜，负值的话，表示的是往右倾斜


## css 中的坐标系

`css` 中的坐标系和数学中的坐标系正好相反

简单记住他们的坐标：

`X`轴左边是负的，右边是正的。

`Y`轴上面是负的，下面是正的。

`Z`里面是负的，外面是正的。


## `CSS3` animation 动画效果







