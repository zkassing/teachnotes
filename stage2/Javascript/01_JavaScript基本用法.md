# JS 在页面中的位置

> 我们可以将`JavaScript`代码放在`html`文件中任何位置

> 但是我们一般放在网页的`head`或者`body`部分。

## 放在`<head>`部分

最常用的方式是在页面中 head 部分放置`<script>`元素，浏览器解析 head 部分就会执行这个代码，然后才解析页面的其余部分。

## 放在`<body>`部分

JavaScript 代码在网页读取到该语句的时候就会执行。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>js使用方式3：外部js</title>
    </head>
    <body>
        <input type="button" value="点击" onclick="hello()" />
        <!-- 很多html页面都可以调用helloworld.js页面 -->
        <script src="./helloworld.js" type="text/javascript" charset="utf-8"></script>
    </body>
</html>
```

> **_注意：位置的不同会影响到实现效果。_**
