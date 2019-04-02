# JS使用方法

HTML 中的脚本必须位于 \<script> 与 \</script> 标签之间。脚本可被放置在 HTML 页面的 \<body> 和 \<head> 部分中。

## \<script> 标签
如需在 HTML 页面中插入 JavaScript，请使用 \<script> 标签。\<script> 和 \</script> 会告诉 JavaScript 在何处开始和结束。\<script> 和 \</script> 之间的代码行包含了JavaScript
```javascript
<script>
alert("My First JavaScript");
</script>
```
## \<head> 中的 JavaScript 函数
```javascript
<!DOCTYPE html>
<html>
    <head>
        <script>
            function myFunction(){
                document.getElementById("demo").innerHTML="My First JavaScript Function";
            }
        </script>
    </head>
    <body>
        <h1>My Web Page</h1>
        <p id="demo">A Paragraph</p>
        <button type="button" onclick="myFunction()">Try it</button>
    </body>
</html>
```

## \<body> 中的 JavaScript 函数
提示：我们把 JavaScript 放到了页面代码的底部，这样就可以确保在 \<p> 元素创建之后再执行脚本。
```javascript
<!DOCTYPE html>
<html>
    <head>
        <title>Hello World!</title>
    </head>
    <body>
        <h1>My Web Page</h1>
        <p id="demo">A Paragraph</p>
        <button type="button" onclick="myFunction()">Try it</button>
        
        <script>
            //如果要在body中使用JavaScript，我们把 JavaScript 放到了页面代码的底部，这样就可以确保在 p 元素创建之后再执行脚本
            function myFunction(){
                document.getElementById("demo").innerHTML="My First JavaScript Function";
            }
        </script>
    </body>
</html>
```
## 外部的 JavaScript
也可以把脚本保存到外部文件中。外部文件通常包含被多个网页使用的代码。外部 JavaScript 文件的文件扩展名是 .js。如需使用外部文件，请在\<script> 标签的 "src" 属性中设置该 .js 文件

提示：外部脚本不能包含 \<script> 标签。

```javascript
<!DOCTYPE html>
<html>
    <body>
        <script src="myScript.js"></script>
    </body>
</html>
```

