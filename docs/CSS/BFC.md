# BFC

> BFC：Block Formatting Context（块级格式化上下文）。确定一种渲染规则，它决定了其子元素如何定位，以及和其他元素的关系和相互作用。 最常见的 Formatting Context 有 **Block formatting context** 和 **Inline formatting context**。  
> BFC 是完全独立的布局空间，空间中的子元素不会影响到外面的布局，从而起到隔离保护作用。如果没有设置高度，会被里面的元素撑开。

## 常见的定位方案

### 1. 普通流

普通流的元素按章 html 的位置从上而下布局。行内元素水平排列，块级元素独占一行。  
不是 float、absolutely position、root element，就是普通流。BFC 也属于普通流。

### 2. 浮动

浮动元素按照普通流的位置出现，按照属性设置向左右浮动。直到接触到 border 或者另一个浮动元素。

### 3. 绝对定位

元素整体脱离普通流。postion: absolute / fixed;

## Box：CSS 布局的基本单位

Box 是 CSS 布局的基本单位，元素的类型和 display 属性，决定了这个 box 的类型。不同的 box，会参与不同的 Formatting Context（一个决定如何渲染文档的容器），因此 box 内的元素会以不同的方式渲染。

常见盒子：

-   块盒 block-level box：_display_ 属性为 **block**，**list-item**，**table** 的元素。此类元素都是独占一行。
-   行盒 inline-level box：_display_ 属性为 **inline**，**inline-block**，**inline-table** 的元素。不独占一行，依次排列。

    > inline 不可以设置上下 margin、padding、border 的宽度，只能设置左右。如果给他加浮动，上下边距就有效。
    > inline-block 与 block 的特性一样，上下左右的边距都可以设置，只是没有独占一行。

-   run-in box：css3 特有

## BFC 布局规则 & 解决问题

-   内部的 Box 会在垂直方向一个接一个地放置，距离由 margin 决定。属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
-   每个盒子（块盒与行盒）的 margin box 的左边，与包含块 border box 的左边相接触，即使存在浮动也是如此
-   BFC 的区域不会与 float box 重叠
-   BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响外面的元素。反之也是如此
-   计算 BFC 的高度时，浮动元素也参与计算

参考：https://juejin.cn/post/6975653973550170126?share_token=e10ab50a-882d-41ce-b5b1-57d5cf6cc6f7

### 1. 脱离文档流：web 网页广告位的固定

`position：absolute / fixed;` absolute 是相对于最近的非静态祖先元素的定位；fixed 是对屏幕窗口（body）的绝对定位。使用 absolute 的广告位向上滑会被划走，但 fixed 不会。
[position 属性: 相对定位、绝对定位](https://www.runoob.com/w3cnote/css-position-static-relative-absolute-fixed.html)

> 四个值：static、relative、absolute、fixed
>
> abslute:
>
> 1. 定位：针对有 position 的 **_父元素_** 定位；没有就针对根元素 html 定位。原来的位置会有其他的元素占据。（display:none）
> 2. 大小：脱离了普通流，根据内容撑开。
>
> relative:
>
> 1. 定位：相对自身定位。
> 2. 大小：还在文档流，大小不变。没有设置宽度就是整个浏览器的宽度。

### 2. 实现两栏布局（清除浮动）

两栏布局，父 div 设置背景图片，包裹左右两栏。当左右两栏设置 float 的时候，父元素高度坍塌不见了。所以设置 overflow，重新创建一个父元素的 BFC，背景回来。

```css
给父元素定一个overflow
/* overflow 定义当一个元素的内容太大而无法适应 块级格式化上下文 时候该做什么 */
overflow: hidden / scroll / auto; /*  visible不行 */

```

### 3. 外边距塌陷

img 的 div 和背景图片的 div 外边距（margin）重合，添加 margin 整个下移了。

给 img 的 div 增加`display: inline-block`
或者给背景图片的 div 增加`display: flex`

## 如何触发 BFC

-   根元素或其他包含他的元素
-   浮动元素（元素的 float 不是 none）
-   绝对定位元素（元素具有 position 为 absolute 或 fixed）
-   内联块（元素具有 `display: inline-block`）
-   表格单元格（元素具有 `display: table-cell `，HTML 表格单元格默认属性）
-   表格标题（元素具有 `display: table-caption`，HTML 表格标题默认属性）
-   具有 overflow 且值不是 visible 的块元素
-   弹性盒子（flex 或 inline-flex）
-   `display: flow-root`
-   `column-span: all`

## BFC 的作用

1.  利用 BFC 避免 margin 重叠
2.  自适应两栏布局
3.  清除浮动
