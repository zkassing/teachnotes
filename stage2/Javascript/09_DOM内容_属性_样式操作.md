# HTML DOM - 修改 HTML 内容

通过 HTML DOM，JavaScript 能够访问 HTML 文档中的每个元素。


###改变 HTML 内容

改变元素内容的最简单的方法是使用 innerHTML 属性。

**实例**

```
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="New text!";
</script>

</body>
</html>

```

该例子中id为p1的p标签里的内容会被替换为“New text！”

****

###改变 HTML 样式

通过 HTML DOM 的style属性，可以访问 HTML 对象的样式对象。


**实例**

```
<html>

<body>
<p id="p2">Hello world!</p>

<script>
document.getElementById("p2").style.color="blue";
</script>

</body>
</html>

```
该例子中id为p2的p标签里的字体颜色会变成蓝色