# JavaScript用法

> HTML中的脚本必须位于`<script></script>`标签之间<br>脚本可被放置在HTML页面的`<body>`和`<head>`部分中

```html
<!DOCTYPE HTML>
<html>
<head>
  <meta charset="utf-8">
  <title>如何使用javascript</title>
  <!-- 
  <script></script>
  -->
</head>
<body>
  <!-- 出于性能考虑，script标签在大多数时候应该放置在body的闭合标签之前 -->
  <script>
    alert('hello world');
  </script>
</body>
</html>
```

## JavaScript编码位置

> JavaScript有两个编码位置，一种是直接将代码写在script标签中，一种是新建单独的js文件存储JavaScript代码，然后在script标签中利用`src`引入
```
- Project
  - js
    - demo.js
  - index.html
```

如果有以上结构，我们可以在HTML中引入对应的js

index.html
```html
<!DOCTYPE HTML>
<html>
<head>
  <meta charset="utf-8">
  <title>如何引入外部js</title>
</head>
<body>
  <script src="./js/demo.js"></script>
</body>
</html>
```
demo.js
```javascript 
alert('这是我的第一个javascript程序');
```

***如果页面上正确弹出对应的对话框，则你的代码就算运行成功了！***
