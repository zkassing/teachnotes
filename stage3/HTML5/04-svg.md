# SVG 
1. 意为可缩放矢量图形（Scalable Vector Graphics）
2. 用来定义用于网络的基于矢量的图形
3. SVG 使用 XML 格式定义图像。
4. 图像在放大或改变尺寸的情况下其图形质量不会有所损失
5. 是万维网联盟的标准
6. SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体

## SVG 的历史和优势
在 2003 年一月，SVG 1.1 被确立为 W3C 标准。

参与定义 SVG 的组织有：太阳微系统、Adobe、苹果公司、IBM 以及柯达。

与其他图像格式相比，使用 SVG 的优势在于：

+ SVG 可被非常多的工具读取和修改（比如记事本）
+ SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
+ SVG 是可伸缩的
+ SVG 图像可在任何的分辨率下被高质量地打印
+ SVG 可在图像质量不下降的情况下被放大
+ SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
+ SVG 可以与 Java 技术一起运行
+ SVG 是开放的标准
+ SVG 文件是纯粹的 XML
+ SVG 的主要竞争者是 Flash。

与 Flash 相比，SVG 最大的优势是与其他标准（比如 XSL 和 DOM）相兼容。而 Flash 则是未开源的私有技术。

## SVG 实例
SVG 文件必须使用 .svg 后缀来保存：
```
<?xml version="1.0" standalone="no"?>

<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>

</svg>
```

## HTML 页面中的 SVG
SVG 文件可通过以下标签嵌入 HTML 文档：embed、object 或者 iframe。
但是推荐大家使用如下方式：
```
<html xmlns:svg="http://www.w3.org/2000/svg">
<body>

<p>This is an HTML paragraph</p>

<svg:svg width="300" height="100" version="1.1" >
<svg:circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red" />
</svg:svg>

</body>
</html>
```

## SVG 有一些预定义的形状元素，可被开发者使用和操作。
### rect 标签
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<rect x="20" y="20"  rx="20" ry="20" width="250" height="250"
style="fill:blue;stroke:pink;stroke-width:5;
fill-opacity:0.1;stroke-opacity:0.9"/>

</svg>
```
+ x 属性定义矩形的左侧位置（例如，x="0" 定义矩形到浏览器窗口左侧的距离是 0px）
+ y 属性定义矩形的顶端位置（例如，y="0" 定义矩形到浏览器窗口顶端的距离是 0px）
+ rx 和 ry 属性可使矩形产生圆角。
+ CSS 的 fill-opacity 属性定义填充颜色透明度（合法的范围是：0 - 1）
+ CSS 的 stroke-opacity 属性定义笔触颜色的透明度（合法的范围是：0 - 1）

### circle 标签可用来创建一个圆。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<circle cx="100" cy="50" r="40" stroke="black"
stroke-width="2" fill="red"/>
```
代码解释：
cx 和 cy 属性定义圆点的 x 和 y 坐标。如果省略 cx 和 cy，圆的中心会被设置为 (0, 0)

r 属性定义圆的半径。
### ellipse 标签可用来创建椭圆。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<ellipse cx="300" cy="150" rx="200" ry="80"
style="fill:rgb(200,100,50);
stroke:rgb(0,0,100);stroke-width:2"/>

</svg>
```
代码解释：
+ cx 属性定义圆点的 x 坐标
+ cy 属性定义圆点的 y 坐标
+ rx 属性定义水平半径
+ ry 属性定义垂直半径

### line 标签用来创建线条。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<line x1="0" y1="0" x2="300" y2="300"
style="stroke:rgb(99,99,99);stroke-width:2"/>

</svg>
```
代码解释：
+ x1 属性在 x 轴定义线条的开始
+ y1 属性在 y 轴定义线条的开始
+ x2 属性在 x 轴定义线条的结束
+ y2 属性在 y 轴定义线条的结束
### polygon 标签用来创建含有不少于三个边的图形。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<polygon points="220,100 300,210 170,250"
style="fill:#cccccc;
stroke:#000000;stroke-width:1"/>

</svg>
```
代码解释：
points 属性定义多边形每个角的 x 和 y 坐标

### polyline 标签用来创建仅包含直线的形状。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<polyline points="0,0 0,20 20,20 20,40 40,40 40,60"
style="fill:white;stroke:red;stroke-width:2"/>

</svg>
```
### path 标签用来定义路径。


下面的命令可用于路径数据：

+ M = moveto
+ L = lineto
+ H = horizontal lineto
+ V = vertical lineto
+ C = curveto
+ S = smooth curveto
+ Q = quadratic Belzier curve
+ T = smooth quadratic Belzier curveto
+ A = elliptical Arc
+ Z = closepath
> 注释：以上所有命令均允许小写字母。大写表示绝对定位，小写表示相对定位。
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<path d="M250 150 L150 350 L350 350 Z" />

</svg>
```
上面的例子定义了一条路径，它开始于位置 250 150，到达位置 150 350，然后从那里开始到 350 350，最后在 250 150 关闭路径。
### SVG 滤镜
在 SVG 中，可用的滤镜有：

+ feBlend
+ feColorMatrix
+ feComponentTransfer
+ feComposite
+ feConvolveMatrix
+ feDiffuseLighting
+ feDisplacementMap
+ feFlood
+ feGaussianBlur
+ feImage
+ feMerge
+ feMorphology
+ feOffset
+ feSpecularLighting
+ feTile
+ feTurbulence
+ feDistantLight
+ fePointLight
+ feSpotLight
注释：您可以在每个 SVG 元素上使用多个滤镜！
### SVG 高斯模糊
> 必须在 defs 标签中定义 SVG 滤镜。
```

<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<defs>
<filter id="Gaussian_Blur">
<feGaussianBlur in="SourceGraphic" stdDeviation="3" />
</filter>
</defs>

<ellipse cx="200" cy="150" rx="70" ry="40"
style="fill:#ff0000;stroke:#000000;
stroke-width:2;filter:url(#Gaussian_Blur)"/>

</svg>
```
代码解释：
+ filter 标签的 id 属性可为滤镜定义一个唯一的名称（同一滤镜可被文档中的多个元素使用）
+ filter:url 属性用来把元素链接到滤镜。当链接滤镜 id 时，必须使用 # 字符
+ 滤镜效果是通过 feGaussianBlur 标签进行定义的。fe 后缀可用于所有的滤镜
+ feGaussianBlur 标签的 stdDeviation 属性可定义模糊的程度
+ in="SourceGraphic" 这个部分定义了由整个图像创建效果

### SVG 线性渐变
SVG 渐变必须在 defs 标签中进行定义。
linearGradient 可用来定义 SVG 的线性渐变。

linearGradient 标签必须嵌套在 defs 的内部。defs 标签是 definitions 的缩写，它可对诸如渐变之类的特殊元素进行定义。

线性渐变可被定义为水平、垂直或角形的渐变：

+ 当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
+ 当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
+ 当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<defs>
<linearGradient id="orange_red" x1="0%" y1="0%" x2="100%" y2="0%">
<stop offset="0%" style="stop-color:rgb(255,255,0);
stop-opacity:1"/>
<stop offset="100%" style="stop-color:rgb(255,0,0);
stop-opacity:1"/>
</linearGradient>
</defs>

<ellipse cx="200" cy="190" rx="85" ry="55"
style="fill:url(#orange_red)"/>

</svg>
```
代码解释：
+ linearGradient 标签的 id 属性可为渐变定义一个唯一的名称
+ fill:url(#orange_red) 属性把 ellipse 元素链接到此渐变
+ linearGradient 标签的 x1、x2、y1、y2 属性可定义渐变的开始和结束位置
+ 渐变的颜色范围可由两种或多种颜色组成。每种颜色通过一个 stop 标签来规定。offset 属性用来定义渐变的开始和结束位置。
### SVG 放射性渐变
```
<svg width="100%" height="100%" version="1.1"
xmlns="http://www.w3.org/2000/svg">

<defs>
<radialGradient id="grey_blue" cx="50%" cy="50%" r="50%"
fx="50%" fy="50%">
<stop offset="0%" style="stop-color:rgb(200,200,200);
stop-opacity:0"/>
<stop offset="100%" style="stop-color:rgb(0,0,255);
stop-opacity:1"/>
</radialGradient>
</defs>

<ellipse cx="230" cy="200" rx="110" ry="100"
style="fill:url(#grey_blue)"/>

</svg>
```
代码解释：
+ radialGradient 标签的 id 属性可为渐变定义一个唯一的名称，
+ fill:url(#grey_blue) 属性把 ellipse 元素链接到此渐变，
+ cx、cy 和 r 属性定义外圈，
+ 而 fx 和 fy 定义内圈 
+ 渐变的颜色范围可由两种或多种颜色组成,每种颜色通过一个 stop 标签来规定。
+ offset 属性用来定义渐变的开始和结束位置。














