# CSS盒模型

*css盒模型属性：width height padding border margin*
1. width 和 height
    - width 取值：
        * width:200px;
        * widht:50%;//百分比是参照父元素的宽度，如果没有父元素，则参照body
    - height 取值：
        * height:300px;//设置固定的高度
        * height:auto;//高度自动，相当于高度有内容来撑
*在 CSS 中，width 和 height 指的是内容区域的宽度和高度。块元素没有设置宽高，宽度继承父元素，高度由内容来撑*
2. padding 内填充 
    - 取值： 
        * padding:10px;//上右下左四个方向值一样；
        * padding：10px 20px; //第一个值是上下   第二个值是左右
        * padding：10px 20px 30px;//第一个值是上  第二个值是左右  第三个值是下
        * padding：10px 20px 30px 40px;第一个值是上  第二个值是右  第三个值是下 第四个值是左
    ***行内元素不支持上下的padding，虽然能撑开，但是不占位，支持左右的padding***
3. border 边框属性
    - 取值：
        * border-style:solid; //边框的样式
        * border-color:red; //边框的颜色
        * border-width:3px; //边框的粗细
        *这是边框样式的拆分写法*
    - 综合属性：
        * border:3px solid red; //（粗细，样式，颜色，顺序不能乱）
***边框的样式双实线double 要求边框的粗细必须大于等于3px才能出现效果***
4. margin 外间距
    - 取值：
        * margin: 10px;//上右下左四个方向值一样；
        * margin：10px 20px; //第一个值是上下   第二个值是左右
        * margin：10px 20px 30px;//第一个值是上  第二个值是左右  第三个值是下
        * margin：10px 20px 30px 40px;第一个值是上  第二个值是右  第三个值是下 第四个值是左
    ***行内元素不支持上下的margin，支持左右的margin***
    ***margin:0 auto;可以让一个有固定宽度且宽度不为100%的块元素水平居中***
# css盒模型的计算
* 一个盒子在页面中真实占有的宽度 = width(设置的宽度) + padding(左边的padding) + border(左边的边框) + margin(左边的margin) + padding(右边的padding)  + border(右边的边框) + margin(右边的margin)

* 一个盒子在页面中真实占有的高度 = height(设置的高度) + padding(上边的padding) + border(上边的边框) + margin(上边的margin) + padding(下的padding)  + border(下边的边框) + margin(下边的margin)



# 标准盒模型和IE盒模型的区别：
* 标准和模型：内容区content（width和height）  padding  border  margin
* IE盒模型：内容区content包括了width height padding 和 border ;
![效果图](image/hmx1.gif)

# 背景属性 background
* background-color :red;//背景颜色属性
* background-image：url(image/bg.jpg);//背景图片属性
* background-position：20px 40px;//背景图片定位
    > 取值方式：
        >> 1、使用px单位；background-position：20px 40px;  
        >> 2、使用关键字，水平方向：left center right ；垂直方向：top center bottom
* background-repeat:背景图片平铺
    - 取值：
       * repeat：平铺
       * no-repeat 不平铺
       * repeat-x 水平方向平铺
       * repeat-y 垂直方向平铺
* background-attachment：背景图片固定
    * 取值：
        - scroll 背景图像会随着页面其余部分的滚动而移动。
        - fixed 当页面的其余部分滚动时，背景图像不会移动




