[toc]

# 官网

> http://www.jquery.com

# 理念

> write less, do more (用更少的代码, 实现更多的功能)

# 成就

全世界排名前 100 万的网站, 有 46%再使用 jquery
远远超过其他库
微软把 jquery 当成他们的官方库

# jquery 的设计思想

## 选择网页元素

css 选择器

-   `$(document) 选择整个文档对象`
-   `$('#myId') 选择 id 为 myId 的网页元素`
-   `$('div.myClass') 选择 class 为 myClass 的 div 元素`

jquery 的特有表达式

-   `$('a:first') 选择网页中第一个 a 元素`
-   `$('tr:odd') 选择表格中的奇数行`
-   `$('div:visible') 选择可见的 div 元素`

方法函数化

`window.onload ==> $()`

`innerHTML ==> html()`

`onclick ==> click()`

```javascript
$(function() {
    $("div").click(function() {
        alert($(this).html());
    });
});
```

原生与 jquery

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"><p>hello world</p></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                alert($(this).html());
            });
        });
    </script>
</html>
```

-   原生 js, jquery 可以共存, 但是, 不能混用

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"><p>hello world</p></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                alert(this.innerHTML); // jquery可以混用js
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"><p>hello world</p></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                alert(this.html()); // 这两种写法都是错的
                alert($(this).innerHTML); // 这两种写法都是错的
            });
        });
    </script>
</html>
```

空前强大的过滤器
`$('div').has('p') // 包含p元素的div元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"><p></p></div>
        <div class="div1"></div>
        <div class="div2"></div>
        <div class="div3"></div>
        <div class="div4"></div>
    </body>
    <script>
        $(function() {
            $("div")
                .has("p")
                .css("border", "1px solid green");
        });
    </script>
</html>
```

`$('div').not('.myClass') // class 不等于 myClass 的 div 元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"></div>
        <div class="div1"></div>
        <div class="div2"></div>
        <div class="div3"></div>
        <div class="div4"></div>
    </body>
    <script>
        $(function() {
            $("div")
                .not(".div3")
                .css("border", "1px solid green");
        });
    </script>
</html>
```

`$('div').filter('.myClass') // 选择 class 等于 myClass 的 div 元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div class="div0"></div>
        <div class="div1"></div>
        <div class="div2"></div>
        <div class="div3"></div>
        <div class="div4"></div>
    </body>
    <script>
        $(function() {
            $("div")
                .filter(".div3")
                .css("border", "1px solid green");
        });
    </script>
</html>
```

相邻元素的查找

`$('div').next('p') // 选择div元素后面的第一个p元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
        </div>
        <h3>this is h3_7</h3>
    </body>
    <script>
        $(function() {
            $("div")
                .next("h3")
                .css("background", "red");
        });
    </script>
</html>
```

> next()也可以没有参数

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
        </div>
        <h3>this is h3_7</h3>
    </body>
    <script>
        $(function() {
            $("div")
                .next()
                .css("background", "red");
        });
    </script>
</html>
```

`$('div').parent(); // 选择 div 元素的父元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
            <h3>this is h3_7</h3>
        </div>
    </body>
    <script>
        $(function() {
            $("h3")
                .parent()
                .css("background", "red");
        });
    </script>
</html>
```

`$('div').children() // 选择 div 的所有子元素`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
            <h3>this is h3_7</h3>
        </div>
    </body>
    <script>
        $(function() {
            $("div")
                .children()
                .css("background", "red");
        });
    </script>
</html>
```

## 链式操作

`$('div').find('h3').eq(2).html('hello')`
相当于...

1. 找到 div
2. 选择其中的 h3 元素
3. 选择第三个 h3
4. 把内容改成 hello

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
            <h3>this is h3_7</h3>
        </div>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h3") // 找到h3
                .eq(2) // 相当于下标2
                .css("background", "red"); // 设置红色背景
        });
    </script>
</html>
```

jquery 提供了 end()方法, 使得结果集可以后退一步

## 一次 div, 往上跳一级

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
            <h3>this is h3_7</h3>
        </div>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h3")
                .eq(2)
                .css("background", "red")
                .end()
                .eq(1)
                .css("background", "yellow"); // 两行都会变色
        });
    </script>
</html>
```

## 可以两次 end()

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h3>this is h3_0</h3>
            <h3>this is h3_1</h3>
            <h3>this is h3_2</h3>
            <h3>this is h3_3</h3>
            <h3>this is h3_4</h3>
            <h3>this is h3_5</h3>
            <h3>this is h3_6</h3>
            <h3>this is h3_7</h3>
        </div>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h3")
                .eq(2)
                .css("background", "red")
                .end()
                .eq(1)
                .css("background", "yellow")
                .end()
                .end()
                .css("border", "1px red solid");
        });
    </script>
</html>
```
