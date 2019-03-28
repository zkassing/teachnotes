# CSSBFC模型
1. 什么是BFC
>BFC全称是Block Formatting Context，即块格式化上下文。它是CSS2.1规范定义的，关于CSS渲染定位的一个概念。要明白BFC到底是什么，首先来看看什么是视觉格式化模型。
2. 视觉格式化模型
> 视觉格式化模型(visual formatting model)是用来处理文档并将它显示在视觉媒体上的机制，它也是CSS中的一个概念。
> 视觉格式化模型定义了盒（Box）的生成，盒主要包括了块盒、行内盒、匿名盒（没有名字不能被选择器选中的盒）以及一些实验性的盒（未来可能添加到规范中）。盒的类型由display属性决定。  
- 块盒（block box）  
    **块盒有以下特性：**
    * 当元素的CSS属性display为block，list-item或table时，它是块级元素 block-level
    * 视觉上呈现为块，竖直排列；
    * 块级盒参与(块格式化上下文)；
    * 每个块级元素至少生成一个块级盒，称为主要块级盒(principal block-level box)。一些元素，比如```<li>```，生成额外的盒来放置项目符号，不过多数元素只生成一个主要块级盒。
- 行内盒（inline box）
    * 当元素的CSS属性display的计算值为inline，inline-block或inline-table时，称它为行内级元素；
    * 视觉上它将内容与其它行内级元素排列为多行；典型的如段落内容，有文本(可以有多种格式譬如着重)，或图片，都是行内级元素；
    * 行内级元素生成行内级盒(inline-level boxes)，参与行内格式化上下文(inline formatting context)。同时参与生成行内格式化上下文的行内级盒称为行内盒(inline boxes)。所有display:inline的非替换元素生成的盒是行内盒；
    * 不参与生成行内格式化上下文的行内级盒称为原子行内级盒(atomic inline-level boxes)。这些盒由可替换行内元素，或 display 值为 inline-block 或 inline-table 的元素生成，不能拆分成多个盒；
- 匿名盒（anonymous box）  
    ***匿名盒也有份匿名块盒与匿名行内盒，因为匿名盒没有名字，不能利用选择器来选择它们，所以它们的所有属性都为inherit或初始默认值；***
3. 三个定位方案  
> 在定位的时候，浏览器就会根据元素的盒类型和上下文对这些元素进行定位，可以说盒就是定位的基本单位。定位时，有三种定位方案，分别是常规流，浮动以及绝对定位。
- 常规流(Normal flow)

    * 在常规流中，盒一个接着一个排列;
    * 在块级格式化上下文里面， 它们竖着排列；
    * 在行内格式化上下文里面， 它们横着排列;
    * 当position为static或relative，并且float为none时会触发常规流；
    * 对于静态定位(static positioning)，position: static，盒的位置是常规流布局里的位置；
    * 对于相对定位(relative positioning)，position: relative，盒偏移位置由这些属性定义top，bottom，leftandright。即使有偏移，仍然保留原有的位置，其它常规流不能占用这个位置。

- 浮动(Floats)

    * 盒称为浮动盒(floating boxes)；
    * 它位于当前行的开头或末尾；
    * 这导致常规流环绕在它的周边，除非设置 clear 属性；

- 绝对定位(Absolute positioning)

    * 绝对定位方案，盒从常规流中被移除，不影响常规流的布局；
    * 它的定位相对于它的包含块，相关CSS属性：top，bottom，left及right；
    * 如果元素的属性position为absolute或fixed，它是绝对定位元素；
    * 对于position: absolute，元素定位将相对于最近的一个relative、fixed或absolute的父元素，如果没有则相对于body；
4. 块级格式化上下文  
*块格式上下文是页面CSS 视觉渲染的一部分，用于决定块盒子的布局及浮动相互影响范围的一个区域。*

5. BFC的创建方法
    * 根元素或其它包含它的元素；
    * 浮动 (元素的float不为none)；
    * 绝对定位元素 (元素的position为absolute或fixed)；
    * 行内块inline-blocks(元素的 display: inline-block)；
    * 表格单元格(元素的display: table-cell，HTML表格单元格默认属性)；

    * overflow的值不为visible的元素；
    * 弹性盒 flex boxes (元素的display: flex或inline-flex)；

***但其中，最常见的就是overflow:hidden、float:left/right、position:absolute。也就是说，每次看到这些属性的时候，就代表了该元素以及创建了一个BFC了。***

6. BFC的作用及原理
- (1) 自适应两栏布局  
　　代码：
```
	<style>
    body {
        width: 300px;
        position: relative;
    }
 
    .aside {
        width: 100px;
        height: 150px;
        float: left;
        background: #f66;
    }
 
    .main {
        height: 200px;
        background: #fcc;
    }
</style>
<body>
    <div class="aside"></div>
    <div class="main"></div>
</body>
```
![效果图](image/bfc1.png)
> BFC的区域不会与float box重叠。
　　我们可以通过通过触发main生成BFC， 来实现自适应两栏布局。
```
.main {
    overflow: hidden;
}
```
![效果图](image/bfc2.png)
- (2)清除内部浮动
```
<style>
    .par {
        border: 5px solid #fcc;
        width: 300px;
    }
 
    .child {
        border: 5px solid #f66;
        width:100px;
        height: 100px;
        float: left;
    }
</style>
<body>
    <div class="par">
        <div class="child"></div>
        <div class="child"></div>
    </div>
</body>
```
> 计算BFC的高度时，浮动元素也参与计算
　　为达到清除内部浮动，我们可以触发par生成BFC，那么par在计算高度时，par内部的浮动元素child也会参与计算。
```
.par {
    overflow: hidden;
}
```

- (3)防止垂直 margin 重叠
```
<style>
    p {
        color: #f55;
        background: #fcc;
        width: 200px;
        line-height: 100px;
        text-align:center;
        margin: 100px;
    }
</style>
<body>
    <p>Haha</p>
    <p>Hehe</p>
</body>
```
> Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠;
我们可以在p外面包裹一层容器，并触发该容器生成一个BFC。那么两个P便不属于同一个BFC，就不会发生margin重叠了。
```
<style>
    .wrap {
        overflow: hidden;
    }
    p {
        color: #f55;
        background: #fcc;
        width: 200px;
        line-height: 100px;
        text-align:center;
        margin: 100px;
    }
</style>
<body>
    <p>Haha</p>
    <div class="wrap">
        <p>Hehe</p>
    </div>
</body>
```
***BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。***


