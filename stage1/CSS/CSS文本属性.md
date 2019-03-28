# CSS文本属性

***CSS 文本属性可定义文本的外观。通过文本属性，您可以改变文本的颜色、字符间距，对齐文本，装饰文本，对文本进行缩进，等等。***
1. 文本首行缩进text-indent  
    - 取值：
        * text-index:20px;
        * text-index:-30px;
        * text-index:5em;
    - 案例:
        ```
        p {text-indent: 5em;}
        ```
        *在为 text-indent 设置负值时要当心，如果对一个段落设置了负值，那么首行的某些文本可能会超出浏览器窗口的左边界。为了避免出现这种显示问题，建议针对负缩进再设置一个外边距或一些内边距：*

2. 文本水平对齐text-align
    - 取值：
        - left：文本左对齐（默认对齐方式）
        - center:文本水平居中
        - right:文本右对齐
        - justify：文本两端对齐（处尾行外都有效果）
    - 案例:
        ```
        p {text-algin: center;}
        ```
    *text-algin: center可以使块元素中行内元素和行内块元素水平居中*

3. 字间隔 word-spacing
*改变字（单词）之间的标准间隔,正直间距变大，赋值间距变小，适用于英文*
    - 案例：
    ```
    p {word-spacing: 30px;}
    ```
4. 字符间距 letter-spacing
*与 word-spacing 的区别在于，字符间隔修改的是字符或字母之间的间隔。中英文都适用*
    - 案例：
    ```
    p {letter-spacing: 30px;}
    ```
5. 文本修饰 text-decoration
    - 取值：
        - none    // 没有下划线
        - underline  // 添加下划线
        - overliner  //文本的顶端画一个上划线
        - line-through  //文本中间画一个贯穿线

    - 案例：
    ```
    a{
        text-decoration:none;//取消下划线
    }
    ```
6. 元素的垂直对齐方式 vertical-align 
    - 取值：
        - baseline //默认值，基线对齐
        - top  //把元素的顶端与行中最高元素的顶端对齐
        - middle  //把此元素放置在父元素的中部。
        - bottom  //把元素的顶端与行中最低的元素的顶端对齐。
        - lenght:使用像素px 如20px;
    *常见用于图片和文本的对齐，行内块元素对齐方式*
    ```
        img{
            vertical-align:middle;
        }
    ```



