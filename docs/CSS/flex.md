# flex

弹性布局，可以给盒状模型最大的灵活性  
`display: flex`  
行内元素也可以使用 flex 布局  
`display: inline-flex`
webkit 内核的浏览器，需要加上-webkit 前缀

```
dislay: -wibkit-flex;
dislay: flex;
```

## flex 容器

指采用 flex 布局的元素

> 1. 两根轴：水平主轴 main axis；垂直交叉轴 cross axis
> 2. 开始和结束位置：main start、cross start
> 3. 宽：main size
> 4. 高：cross size

## 容器属性

### flex-direction 主轴方向

项目排列方向

![flex-direction](../../img/felx/flex1.png)
column-reverse ---- column ------------------- row ------------------- row-reverse

### flex-wrap

如何换行

1. no-wrap（默认）：不换行
2. wrap：向下换行
3. wrap-reverse：向上换行

![flex-wrap](../../img//felx/flex2.png)

### justify-content

main 轴线的对齐方式，

![justify-content](../../img/felx/flex3.png)

space-between：两端对齐，项目之间的间隔都相等。

space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
