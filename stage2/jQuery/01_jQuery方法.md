# jquery 简介

## 什么是 jquery?

-   **一个 js 库, 大型开发必备**
-   **相当于 js 升级版**

## jquery 的好处

> 如果把编程比喻成做菜...

-   **简化原生 js 操作**
-   **不用担心兼容性**
-   **提供大量的实用方法**

## 如何学习 jquery

-   **jquery 只是辅助工具, 要正确面对(佐料齐了...)**
-   **原生 js 和 jquery 都要会(学了英语就不会汉语了?)(原生 js 是基础)**
-   **先易后难...**

# jquery 的设计思想-选择元素

## 选择网页元素

-   **模拟 css 选择元素**

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div id="div1" class="box">div</div>
    </body>
    <script>
        // 三种方式, 都能找到对象
        $(function() {
            $("#div1").css("background", "red");
            // $("div").css("background", "yellow");
            // $(".box").css("background", "blue");
        });
    </script>
</html>
```

_jquery 省略了循环..._

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
    </body>
    <script>
        // jquery省略了循环
        $(function() {
            $(".box").css("background", "blue");
        });
    </script>
</html>
```

-   **独有的表达式选择**

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
    </body>
    <script>
        $(function() {
            $(".box:first").css("background", "blue"); // 第一个div会变蓝...
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
    </body>
    <script>
        $(function() {
            $(".box:last").css("background", "blue"); // 最后一个div会变蓝...
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
        <div class="box">div</div>
    </body>
    <script>
        $(function() {
            $(".box:eq(2)").css("background", "blue"); // 第三个div会变蓝...
            $(".box")
                .eq(1)
                .css("background", "yellow"); // 第二个div会变黄...
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li 0</li>
            <li>this is li 1</li>
            <li>this is li 2</li>
            <li>this is li 3</li>
            <li>this is li 4</li>
            <li>this is li 5</li>
            <li>this is li 6</li>
            <li>this is li 7</li>
            <li>this is li 8</li>
            <li>this is li 9</li>
        </ul>
    </body>
    <script>
        $("li:odd").css("background", "blue"); // 隔行换色, 奇数行
        // $("li:even").css("background", "blue"); // 隔行换色, 偶数行
    </script>
</html>
```

-   **多种筛选方法**

_根据 div 找对象的两种方法_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li class="li">this is li 0</li>
            <li class="li li1">this is li 1</li>
            <li class="li li1">this is li 2</li>
            <li class="li">this is li 3</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li")
                .filter(".li1")
                .css("background", "yellow");
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li class="li">this is li 0</li>
            <li class="li li1">this is li 1</li>
            <li class="li li1">this is li 2</li>
            <li class="li">this is li 3</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li.li1").css("background", "yellow");
        });
    </script>
</html>
```

_过滤器支持属性值_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li title="hello" class="li">this is li 0</li>
            <li class="li li1">this is li 1</li>
            <li class="li li1">this is li 2</li>
            <li title="hello" class="li">this is li 3</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li")
                .filter("[title=hello]")
                .css("background", "yellow");
        });
    </script>
</html>
```

_过滤器, 支持自定义属性_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li tittle="hello" class="li">this is li 0</li>
            <li class="li li1">this is li 1</li>
            <li class="li li1">this is li 2</li>
            <li tittle="hello" class="li">this is li 3</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li")
                .filter("[tittle=hello]")
                .css("background", "yellow");
        });
    </script>
</html>
```

_也可以不要过滤器_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li tittle="hello" class="li">this is li 0</li>
            <li class="li li1">this is li 1</li>
            <li class="li li1">this is li 2</li>
            <li tittle="hello" class="li">this is li 3</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li[tittle=hello]").css("background", "yellow");
        });
    </script>
</html>
```

## jquery 写法

-   **方法函数化**

点击获取 div 内的 html 内容...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div><p>hello world</p></div>
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

_jquery 中基本不用等号_

_几乎所有的操作, 都需要加上括号_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div><p>hello world</p></div>
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

-   **强大的链式操作**

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1"></div>
    </body>
    <script>
        $(function() {
            var oDiv = $("#div1");
            oDiv.html("hello");
            oDiv.css("background", "red");
            $("div").click(function() {
                alert("hello world");
            });
        });
    </script>
</html>
```

_链式操作_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1"></div>
    </body>
    <script>
        $(function() {
            // var oDiv = $("#div1");l
            // oDiv.html("hello");
            // oDiv.css("background", "red");
            // $("div").click(function() {
            //     alert("hello world");
            // });
            $("#div1")
                .html("hello")
                .css("background", "red")
                .click(function() {
                    alert("hello world");
                });
        });
    </script>
</html>
```

-   **取值赋值合体**(方法重载)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1">hello world</div>
    </body>
    <script>
        $(function() {
            alert($("div").html()); // 没有参数就取值
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1">hello world</div>
    </body>
    <script>
        $(function() {
            $("div").html("hello China"); // 有参数就赋值
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1">hello world</div>
    </body>
    <script>
        $(function() {
            console.log($("div").css("width")); // 一两个参数就赋值
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div id="div1">hello world</div>
    </body>
    <script>
        $(function() {
            $("div").css("width", "300px"); // 两个参数就赋值
        });
    </script>
</html>
```

_如果是一堆元素呢?_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li tag 0</li>
            <li>this is li tag 1</li>
            <li>this is li tag 2</li>
            <li>this is li tag 3</li>
            <li>this is li tag 4</li>
            <li>this is li tag 5</li>
            <li>this is li tag 6</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li").css("background", "yellow");
        });
    </script>
</html>
```

如果取值, 取第一个

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li tag 0</li>
            <li>this is li tag 1</li>
            <li>this is li tag 2</li>
            <li>this is li tag 3</li>
            <li>this is li tag 4</li>
            <li>this is li tag 5</li>
            <li>this is li tag 6</li>
        </ul>
    </body>
    <script>
        $(function() {
            console.log($("li").html());
        });
    </script>
</html>
```

## jquery 和原生 js 的关系(公共厕所...)

-   **可以共存, 不能混用**

可以一行 jquery, 一行原生
不能一行里面,既有 jquery, 又有原生...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
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
        <div><p>hello world</p></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                alert($(this).innerHTML); // 不能混用
                alert(this.html()); // 不能混用
            });
        });
    </script>
</html>
```

## `$()`下的常用方法

### `has()`(包含)看元素里面的东西...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">
            div1
            <span>span1</span>
        </div>
        <div>div2</div>
    </body>
    <script>
        $(function() {
            $("div")
                .has("span")
                .css("background", "red");
        });
    </script>
</html>
```

_只能是儿子吗?_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">
            div1
            <span>
                span1
                <span class="span1"></span>
            </span>
        </div>
        <div>div2</div>
    </body>
    <script>
        $(function() {
            $("div")
                .has("span.span1")
                .css("background", "red");
        });
    </script>
</html>
```

### `not()`(对象是当前元素)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div1</div>
        <div>div2</div>
    </body>
    <script>
        $(function() {
            $("div")
                .not(".box")
                .css("background", "red");
        });
    </script>
</html>
```

### `filter()`(反义词是`not()`, 对象同样是当前元素)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">div1</div>
        <div>div2</div>
    </body>
    <script>
        $(function() {
            $("div")
                .filter(".box")
                .css("background", "red");
        });
    </script>
</html>
```

## 注意 has 和 filter 的区别(对象不同)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">this is div</div>
        <div><span class="box">this is span</span></div>
    </body>
    <script>
        $(function() {
            $("div")
                .has(".box")
                .css("background", "red");
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box">this is div</div>
        <div><span class="box">this is span</span></div>
    </body>
    <script>
        $(function() {
            $("div")
                .filter(".box")
                .css("background", "red");
        });
    </script>
</html>
```

### `next()` (下一个兄弟节点) 

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is a div tag</div>
        <span>this is a span tag</span>
        <p>this is a p tag</p>
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

_可以连写吗?_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is a div tag</div>
        <span>this is a span tag</span>
        <p>this is a p tag</p>
    </body>
    <script>
        $(function() {
            $("div")
                .next()
                .next()
                .css("background", "red");
        });
    </script>
</html>
```

### `prev()` (上一个兄弟节点)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is a div tag</div>
        <span>this is a span tag</span>
        <p>this is a p tag</p>
    </body>
    <script>
        $(function() {
            $("p")
                .prev()
                .prev()
                .css("background", "red");
        });
    </script>
</html>
```

### `find()`(查找)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h2>this is a tag h2_1</h2>
            <h2>this is a tag h2_2</h2>
            <h2>this is a tag h2_3</h2>
            <h2>this is a tag h2_4</h2>
            <h3>this is a tag h3_1</h3>
            <h3>this is a tag h3_2</h3>
            <h3>this is a tag h3_3</h3>
            <h3>this is a tag h3_4</h3>
        </div>
        <h2>this is a tag h2_4</h2>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h2")
                .css("background", "red");
        });
    </script>
</html>
```

### `eq()`(下标)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h2>this is a tag h2_1</h2>
            <h2>this is a tag h2_2</h2>
            <h2>this is a tag h2_3</h2>
            <h2>this is a tag h2_4</h2>
            <h3>this is a tag h3_1</h3>
            <h3>this is a tag h3_2</h3>
            <h3>this is a tag h3_3</h3>
            <h3>this is a tag h3_4</h3>
        </div>
        <h2>this is a tag h2_4</h2>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h2")
                .eq(2)
                .css("background", "red");
        });
    </script>
</html>
```

_另一种写法(`:`表示修饰)_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h2>this is a tag h2_1</h2>
            <h2>this is a tag h2_2</h2>
            <h2>this is a tag h2_3</h2>
            <h2>this is a tag h2_4</h2>
            <h3>this is a tag h3_1</h3>
            <h3>this is a tag h3_2</h3>
            <h3>this is a tag h3_3</h3>
            <h3>this is a tag h3_4</h3>
        </div>
        <h2>this is a tag h2_4</h2>
    </body>
    <script>
        $(function() {
            $("div")
                .find("h2:eq(1)")
                .css("background", "red");
        });
    </script>
</html>
```

### `index()`(兄弟中的排行)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <h2>this is a tag h2_1</h2>
            <h2>this is a tag h2_2</h2>
            <h2>this is a tag h2_3</h2>
            <h2>this is a tag h2_4</h2>
            <h3 id="h3">this is a tag h3_1</h3>
            <h3>this is a tag h3_2</h3>
            <h3>this is a tag h3_3</h3>
            <h3>this is a tag h3_4</h3>
        </div>
    </body>
    <script>
        $(function() {
            console.log($("#h3").index());
        });
    </script>
</html>
```

### `attr()`

一个参数取值

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div title="123"></div>
    </body>
    <script>
        $(function() {
            alert($("div").attr("title"));
        });
    </script>
</html>
```

两个参数赋值

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div title="123"></div>
    </body>
    <script>
        $(function() {
            alert($("div").attr("title", "45678"));
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div title="123"></div>
    </body>
    <script>
        $(function() {
            alert(
                $("div")
                    .attr("title", "45678")
                    .attr("class", "box")
            );
        });
    </script>
</html>
```

## 编写一个选项卡

> 原生能写, jquery 就能写, 而且更快,

_先来原生的_

先来布局

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            #div1 div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
                display: none;
            }
            #div1 div:first-of-type {
                display: block;
            }
            .active {
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1">
            <input class="active" type="button" value="button1" />
            <input type="button" value="button2" />
            <input type="button" value="button3" />
            <div>00001</div>
            <div>00002</div>
            <div>00003</div>
        </div>
    </body>
</html>
```

再写 js

```javascript
window.onload = function() {
    var oDiv = document.getElementById("div1");
    var aInput = oDiv.getElementsByTagName("input");
    var aCon = oDiv.getElementsByTagName("div");

    for (var i = 0; i < aInput.length; i++) {
        aInput[i].index = i;
        aInput[i].onclick = function() {
            for (var i = 0; i < aInput.length; i++) {
                aInput[i].className = "";
                aCon[i].style.display = "none";
            }
            this.className = "active";
            aCon[this.index].style.display = "block";
        };
    }
};
```

同样的 html, 再写 jquery

```javascript
$(function() {
    $("#div1")
        .find("input")
        .click(function() {
            $("#div1")
                .find("input")
                .attr("class", "");
            $("#div1")
                .find("div")
                .css("display", "none");
            $(this).attr("class", "active");
            $("#div1")
                .find("div")
                .eq($(this).index())
                .css("display", "block");
        });
});
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            #div1 div {
                width: 200px;
                height: 200px;
                border: 1px solid red;
                display: none;
            }
            #div1 div:first-of-type {
                display: block;
            }
            .active {
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1">
            <input index="0" class="active" type="button" value="button1" />
            <input index="1" type="button" value="button2" />
            <input index="2" type="button" value="button3" />
            <div>00001</div>
            <div>00002</div>
            <div>00003</div>
        </div>
    </body>
    <script>
        $(function() {
            $("#div1")
                .find("input")
                .click(function() {
                    $("#div1")
                        .find("input")
                        .attr("class", "");
                    $(this).attr("class", "active");
                    $("#div1")
                        .find("div")
                        .css("display", "none");
                    $("#div1")
                        .find("div")
                        .eq($(this).attr("index"))
                        .css("display", "block");
                });
        });
    </script>
</html>
```

## `$()下的常用方法`

-   `addClass()` `removeClass()`

> 添加删除样式

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box1 box2"></div>
    </body>
    <script>
        $(function() {
            $("div").addClass("box3 box4");
        });
    </script>
</html>
```

_如果添加的 class 名称, 已经存在了, 会重复吗?_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box1 box2 box3"></div>
    </body>
    <script>
        $(function() {
            $("div").addClass("box3 box4");
        });
    </script>
</html>
```

删除类名

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box1 box2 box3"></div>
    </body>
    <script>
        $(function() {
            $("div").removeClass("box3");
        });
    </script>
</html>
```

_如果类名没有呢?_

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div class="box1 box2 box3"></div>
    </body>
    <script>
        $(function() {
            $("div").removeClass("box3 box4");
        });
    </script>
</html>
```

-   `width()` `innerWidth()` `outerWidth()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            alert($("div").width());
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            alert($("div").css("width"));
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            console.log($("div").width());
            console.log($("div").innerWidth());
            console.log($("div").outerWidth());
        });
    </script>
</html>
```

加一个 padding...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
                padding: 20px;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            console.log($("div").width());
            console.log($("div").innerWidth());
            console.log($("div").outerWidth());
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
                padding: 20px;
                border: 20px solid black;
                margin: 20px;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            console.log($("div").width());
            console.log($("div").innerWidth());
            console.log($("div").outerWidth());
            console.log($("div").outerWidth(true));
        });
    </script>
</html>
```

`console.log($("div").width()); // width`

`console.log($("div").innerWidth()); // width+padding`

`console.log($("div").outerWidth()); // width+padding+border`

`console.log($("div").outerWidth(true)); // width+padding+border+margin`

-   `height()` `innerHeight()` `outerHeight()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 100px;
                background: red;
                padding: 20px;
                border: 20px solid black;
                margin: 20px;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            console.log($("div").height());
            console.log($("div").innerHeight());
            console.log($("div").outerHeight());
            console.log($("div").outerHeight(true));
        });
    </script>
</html>
```

-   `insertBefore()` `before()`

a insertBefore b, 把 a 插入达到 b 的前面 (a,b)
a before b, a 的前面是 b (b,a)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("span").insertBefore($("div"));
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span</span>
        <div>this is div</div>
    </body>
    <script>
        $(function() {
            $("span").before($("div"));
        });
    </script>
</html>
```

-   `insertAfter()` `after()`

a insertAfter b 把 a 插到 b 的后面, (b,a)
a after b a 的后面有个 b, (a,b)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span</span>
        <div>this is div</div>
    </body>
    <script>
        $(function() {
            $("span").insertAfter($("div"));
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("span").after($("div"));
        });
    </script>
</html>
```

-   `appendTo()` `append()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span</span>
        <div>this is div</div>
    </body>
    <script>
        $(function() {
            $("span").appendTo($("div")); // div.appendChild(span)
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("span").append($("div")); // span.appendChild(div)
        });
    </script>
</html>
```

-   `prependTo()` `prepend()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span</span>
        <div>this is div</div>
    </body>
    <script>
        $(function() {
            $("span").prependTo($("div")); // span作为div的第一个孩子
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("div").prepend($("span")); // span作为div的第一个孩子
        });
    </script>
</html>
```

**这些方法区别何在?**(后续操作不同)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("div")
                .before($("span"))
                .css("background", "red");
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("span")
                .insertBefore($("div"))
                .css("background", "red");
        });
    </script>
</html>
```

-   `remove()` 删除节点

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is div</div>
        <span>this is span</span>
    </body>
    <script>
        $(function() {
            $("span").remove();
        });
    </script>
</html>
```

-   `on()` `off()` 事件

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            document.getElementsByTagName("div")[0].onclick = function() {
                alert("hello world");
            };
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                alert("hello jquery");
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("click", function() {
                alert("has clicked");
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("mouseover", function() {
                alert("has overed");
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("mouseover click", function() {
                alert("has done");
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on({
                click: function() {
                    alert("clicked");
                },
                mouseover: function() {
                    alert("overed");
                }
            });
        });
    </script>
</html>
```

off 关闭事件

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("mouseover click", function() {
                alert("has done");
                $("div").off();
            });
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #0f0;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("mouseover click", function() {
                alert("has done");
                $("div").off("click");
            });
        });
    </script>
</html>
```


## `scrollTop()` 获取距离 top 的滚动距离

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            body {
                height: 20000px;
            }
        </style>
    </head>
    <body>
        <script>
            $(function() {
                $(document).click(function() {
                    alert($(window).scrollTop());
                });
            });
        </script>
    </body>
</html>
```

## 编写弹窗

### 增加 div 标签

#### 原生 js 写法

```javascript
window.onload = function() {
    var oDiv = document.createElement("div");
    oDiv.innerHTML = "hello world";
    document.body.appendChild(oDiv);
};
```

#### jquery 写法

```javascript
$(function() {
    var oDiv = $("<div>hello world</div>");
    $("body").append(oDiv);
});
```

## 点击注册, 弹出弹框

#### 先布局

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            #login {
                width: 300px;
                height: 300px;
                border: 1px #000 solid;
                position: absolute;
            }
            #close {
                right: 0;
                top: 0;
                position: absolute;
                background: #ccc;
            }
        </style>
    </head>
    <body>
        <input type="button" value="注册" id="input1" />
        <div id="login">
            <p>
                用户名
                <input type="text" />
            </p>
            <p>
                密码
                <input type="text" />
            </p>
            <div id="close">关闭</div>
        </div>
    </body>
</html>
```

写 js, 点击显示(动态写入 html 代码)

> [备忘]需要手敲, 帮助同学们加深理解...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            #login {
                width: 300px;
                height: 300px;
                border: 1px #000 solid;
                position: absolute;
            }
            #close {
                right: 0;
                top: 0;
                position: absolute;
                background: #ccc;
            }
        </style>
    </head>
    <body>
        <input type="button" value="注册" id="input1" />
    </body>
    <script>
        var str = "";
        $(function() {
            $("#input1").click(function() {
                if (!str) {
                    str += '<div id="login">';
                    str += "<p>";
                    str += "用户名";
                    str += '<input type="text" />';
                    str += "</p>";
                    str += "<p>";
                    str += "密码";
                    str += '<input type="text" />';
                    str += "</p>";
                    str += '<div id="close">关闭</div>';
                    str += "</div>";
                    var oDiv = $(str);
                    $("body").append(oDiv);
                }
            });
        });
    </script>
</html>
```

设置 div 垂直水平居中

```javascript
oDiv.css("left", ($(window).width() - oDiv.outerWidth()) / 2);
```

设置 div 垂直居中

```javascript
oDiv.css("top", ($(window).height() - oDiv.outerHeight()) / 2);
```

设置有滚动条时的垂直居中

```javascript
$(window).on("resize scroll", function() {
    oDiv.css("left", ($(window).width() - oDiv.outerWidth()) / 2);
    oDiv.css(
        "top",
        ($(window).height() - oDiv.outerHeight()) / 2 + $(window).scrollTop()
    );
});
```

给关闭按钮添加功能

```javascript
// 给关闭按钮添加功能
$("#close").on({
    click: function() {
        oDiv.remove();
        str = "";
    },
    mouseover: function() {
        $(this).css("cursor", "pointer");
    }
});
```

## (加戏) `$(document)`,`$(window)`,`$('body')`的区别

document 文档

window 浏览器窗口

body 标签

如果有滚动条, window 的宽度会加上滚动条的宽度

window 的高度, 是展示给用户的高度, 而 document 和 body 是实际高度

## scrollTop

scrollTop 的最大值 = document 的高度 - window 的高度

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
            }
            body {
                height: 2000px;
            }
        </style>
    </head>
    <body></body>
    <script>
        $(function() {
            // console.log("$(document).width");
            // console.log($(document).width());
            // console.log("$(document).outerWidth");
            // console.log($(document).outerWidth());
            // console.log("$(window).width");
            // console.log($(window).width());
            // console.log("$(window).outerWidth");
            // console.log($(window).outerWidth());
            // console.log('$("body").width');
            // console.log($("body").width());
            // console.log('$("body").outerWidth');
            // console.log($("body").outerWidth());
            console.log("$(document).height");
            console.log($(document).height());
            console.log("$(document).outerHeight");
            console.log($(document).outerHeight());
            console.log("$(window).height");
            console.log($(window).height());
            console.log("$(window).outerHeight");
            console.log($(window).outerHeight());
            console.log('$("body").height');
            console.log($("body").height());
            console.log('$("body").outerHeight');
            console.log($("body").outerHeight());
        });
    </script>
</html>
```

## `one`()--事件只执行一次

原来的点击事件, 每次点击, 都会执行

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                height: 200px;
                width: 200px;
                border: 1px solid red;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            $("div").on("click", function() {
                alert("hello world");
            });
        });
    </script>
</html>
```

只执行一次的写法

```javascript
$(function() {
    $("div").one("click", function() {
        alert("hello world");
    });
});
```

## `offset`() `position`()

什么是 offset?

先布局

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
            }
            #div1 {
                width: 200px;
                height: 200px;
                background-color: red;
                overflow: hidden;
                margin: 20px;
            }
            #div2 {
                width: 100px;
                height: 100px;
                background-color: yellow;
                margin: 30px;
            }
        </style>
    </head>
    <body>
        <div id="div1"><div id="div2"></div></div>
    </body>
</html>
```

再写 js

```javascript
$(function() {
    console.log(document.getElementById("div2").offsetLeft);
});
```

如果父级有定位的话, 值还会变...

```css
#div1 {
    width: 200px;
    height: 200px;
    background-color: red;
    overflow: hidden;
    margin: 20px;
    position: relative;
}
```

所以如果想获取到左边屏幕的距离, 你还需要先判断父级是否有定位, 然后需要加上父级到屏幕的距离, 如果父级还有父级呢?

```javascript
$(function() {
    console.log($("#div2").offset().left);
});
```

## `offsetParent`() `parent()`

parent 获取父级

offsetParent 获取有定位的父级

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
            }
            #div1 {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
            #div2 {
                width: 100px;
                height: 100px;
                border: 1px solid green;
            }
        </style>
    </head>
    <body>
        <div id="div1"><div id="div2"></div></div>
        <script>
            $(function() {
                $("#div2")
                    .parent()
                    .css("background", "red");
            });
        </script>
    </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
            }
            #div1 {
                width: 200px;
                height: 200px;
                border: 1px solid red;
            }
            #div2 {
                width: 100px;
                height: 100px;
                border: 1px solid green;
            }
        </style>
    </head>
    <body>
        <div id="div1"><div id="div2"></div></div>
        <script>
            $(function() {
                $("#div2")
                    .offsetParent()
                    .css("background", "red");
            });
        </script>
    </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
            }
            #div1 {
                width: 200px;
                height: 200px;
                border: 1px solid red;
                /* position: relative; */
                /* position: fixed; */
                position: absolute;
            }
            #div2 {
                width: 100px;
                height: 100px;
                border: 1px solid green;
            }
        </style>
    </head>
    <body>
        <div id="div1"><div id="div2"></div></div>
        <script>
            $(function() {
                $("#div2")
                    .offsetParent()
                    .css("background", "red");
            });
        </script>
    </body>
</html>
```

## `val`()

value 值, 没有参数表示取值, 有参数表示赋值

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <input type="button" value="123" />
    </body>
    <script>
        $(function() {
            console.log($("input").val());
        });
    </script>
</html>
```

```javascript
$(function() {
    $("input").val(456);
});
```

## `size`() 获取一组元素的长度

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is tag li1</li>
            <li>this is tag li2</li>
            <li>this is tag li3</li>
            <li>this is tag li4</li>
        </ul>
    </body>
    <script>
        $(function() {
            alert($("li").size());
        });
    </script>
</html>
```

注意 jquery 版本

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is tag li1</li>
            <li>this is tag li2</li>
            <li>this is tag li3</li>
            <li>this is tag li4</li>
        </ul>
    </body>
    <script>
        $(function() {
            alert($("li").length);
        });
    </script>
</html>
```

## `each`() jquery 的循环

-   `each()` 是 jquery 的循环
-   `each()` 接收一个函数做参数, 函数有两个参数, key, value
-   `key` 是下标
-   `value` 是一个对象

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is tag li1</li>
            <li>this is tag li2</li>
            <li>this is tag li3</li>
            <li>this is tag li4</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li").each(function(key, value) {
                console.log("li's key: " + key + ", " + "li's value: " + value);
                console.log(value.innerHTML);
            });
        });
    </script>
</html>
```

## ev 对象, 记录了事件的一些信息

`ev.data.name` // 传递参数
`ev.target` // 当前操作的事件源
`ev.type` // 当前操作的事件类型

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="js/jquery.js"></script>
        <script>
            $(function() {
                $("#div1").on("click", { name: "hello" }, function(ev) {
                    console.log(ev.data.name); // 传递参数
                    console.log(ev.target); // 当前操作的事件源
                    console.log(ev.type); // 当前操作的事件类型
                });
            });
        </script>
    </head>
    <body>
        <div id="div1">aaaa</div>
    </body>
</html>
```

`event.pageX` 和 `event.pageY`：获取鼠标当前相对于页面的坐标
可以确定元素在当前页面的坐标值，是以页面为参考点

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="js/jquery.js"></script>
        <script>
            $(function() {
                $(document).on("mousemove", function(ev) {
                    console.log(ev.pageX + "," + ev.pageY);
                });
            });
        </script>
    </head>
    <body></body>
</html>
```

pageX pageY clientX clientY screenX screenY

pageX pageY 距离文档左上角的 x,y(受滚动条影响)

clientX clientY 当前文档的可视区域的左上角(不受滚动条影响)

screenX screenY 到整个显示器的左上角 x,y

## 编写拖拽

先布局

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: red;
                position: relative;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>
</html>
```

```javascript
$(function() {
    var disX = 0;
    var disY = 0;
    $("div").mousedown(function(ev) {
        disX = ev.pageX - $(this).offset().left;
        disY = ev.pageY - $(this).offset().top;
        $(document).mousemove(function(ev) {
            $("div").css("left", ev.pageX - disX);
            $("div").css("top", ev.pageY - disY);
        });
        $(document).mouseup(function() {
            $(document).off();
        });
        return false;
    });
});
```

## 简单动画

### `hover`()

鼠标移入移出的一个结合版

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
            }
            #div1 {
                background: red;
            }
            #div2 {
                background: blue;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
        <div id="div2"></div>
    </body>
    <script>
        $(function() {
            $("#div1").hover(
                function() {
                    $("#div2").css("background", "yellowgreen");
                },
                function() {
                    $("#div2").css("background", "blue");
                }
            );
        });
    </script>
</html>
```

### `show`() `hide`()

show ==> display:block

hide ==> display:none

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
            }
            #div1 {
                background: red;
            }
            #div2 {
                background: blue;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
        <div id="div2"></div>
    </body>
    <script>
        $(function() {
            $("#div1").hover(
                function() {
                    $("#div2").hide();
                },
                function() {
                    $("#div2").show();
                }
            );
        });
    </script>
</html>
```

可以接收时间作为参数

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").hide(7000);
        },
        function() {
            $("#div2").show(7000);
        }
    );
});
```

### `fadeIn`() `fadeOut`() 淡入 淡出

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").fadeOut();
        },
        function() {
            $("#div2").fadeIn();
        }
    );
});
```

也可以设置时间(默认 400)

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").fadeOut(7000);
        },
        function() {
            $("#div2").fadeIn(7000);
        }
    );
});
```

### `slideDown`() `slideUp`() 向下展开, 向上卷起

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").slideUp();
        },
        function() {
            $("#div2").slideDown();
        }
    );
});
```

同样可以设置时间

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").slideUp(7000);
        },
        function() {
            $("#div2").slideDown(7000);
        }
    );
});
```

### `fadeTo`()

给淡入淡出一个结束点

两个参数, 一个是时间, 一个是透明度

```javascript
$(function() {
    $("#div1").hover(
        function() {
            $("#div2").fadeTo(7000, 0.1, function() {
                alert("完事儿!!!!");
            });
        },
        function() {
            $("#div2").fadeTo(5000, 1, function() {
                alert("变回来了!!!!");
            });
        }
    );
});
```

## `get`()

原生 js 和 jquery 真的不能混用吗?

比如要弹出元素内容...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>this is a div tag</div>
    </body>
    <script>
        $(function() {
            alert($("div").html());
        });
    </script>
</html>
```

get: 把 jquery 转成原生 js

```javascript
$(function() {
    alert($("div").get(0).innerHTML);
});
```

再来试试 li 循环, 注意 get 不加参数, 表示一个集合

```javascript
console.log($("li"));
console.log($("li").get());
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is a li tag 1</li>
            <li>this is a li tag 2</li>
            <li>this is a li tag 3</li>
            <li>this is a li tag 4</li>
            <li>this is a li tag 5</li>
            <li>this is a li tag 6</li>
            <li>this is a li tag 7</li>
            <li>this is a li tag 8</li>
            <li>this is a li tag 9</li>
            <li>this is a li tag 10</li>
        </ul>
    </body>
    <script>
        $(function() {
            for (var i = 0; i < $("li").get().length; i++) {
                console.log($("li").get(i).innerHTML);
            }
        });
    </script>
</html>
```

如果我把`get`去掉呢?

```javascript
$(function() {
    for (var i = 0; i < $("li").length; i++) {
        console.log($("li").get(i).innerHTML);
    }
});
```

注意, `console.log($('li'))`, 会发现`length`属性

如果是下标呢?

```javascript
$(function() {
    for (var i = 0; i < $("li").length; i++) {
        console.log($("li")[i].innerHTML);
    }
});
```

注意`$('li')[0]`和`$('li').eq(0)`的区别

如果想给第一个 li 设置背景...

## `outerWidth`() width+padding+border, 如果是 true, 再加上 margin

原生的 offsetWidth width+padding+border

他俩最根本的区别...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>

    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            alert($("div").outerWidth());
        });
    </script>
</html>
```

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>

    <body>
        <div></div>
    </body>
    <script>
        $(function() {
            alert($("div")[0].offsetWidth);
        });
    </script>
</html>
```

当 display:none 的时候...

offsetWidth ==> 0
jquery 的 outerWidth 依然有值

`visibility: hidden;` 呢?

## `text`()

先看看 text()和 html()的区别

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div><p>hello world</p></div>
    </body>
    <script>
        $(function() {
            console.log($("div").html());
            console.log($("div").text());
        });
    </script>
</html>
```

如果 div 比较多呢...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div><p>hello world_0</p></div>
        <div><p>hello world_1</p></div>
        <div><p>hello world_2</p></div>
        <div><p>hello world_3</p></div>
        <div><p>hello world_4</p></div>
        <div><p>hello world_5</p></div>
        <div><p>hello world_6</p></div>
        <div><p>hello world_7</p></div>
        <div><p>hello world_8</p></div>
        <div><p>hello world_9</p></div>
        <div><p>hello world_10</p></div>
        <div><p>hello world_11</p></div>
        <div><p>hello world_12</p></div>
        <div><p>hello world_13</p></div>
    </body>
    <script>
        $(function() {
            console.log($("div").html());
            console.log($("div").text());
        });
    </script>
</html>
```

那再试试赋值?

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div><p>hello world_0</p></div>
        <div><p>hello world_1</p></div>
        <div><p>hello world_2</p></div>
        <div><p>hello world_3</p></div>
        <div><p>hello world_4</p></div>
        <div><p>hello world_5</p></div>
        <div><p>hello world_6</p></div>
        <div><p>hello world_7</p></div>
        <div><p>hello world_8</p></div>
        <div><p>hello world_9</p></div>
        <div><p>hello world_10</p></div>
        <div><p>hello world_11</p></div>
        <div><p>hello world_12</p></div>
        <div><p>hello world_13</p></div>
    </body>
    <script>
        $(function() {
            var str = "<p>hello China</p>";
            // console.log($("div").html(str));
            console.log($("div").text(str));
        });
    </script>
</html>
```

## `remove`() : `detach`() 这两个都是删除节点

先试试自杀...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: red;
            }
        </style>
    </head>
    <body>
        <div></div>
        <script>
            $(function() {
                $("div").remove();
            });
        </script>
    </body>
</html>
```

删除操作, 会返回操作的值, 如果自杀之前, 已经有点击事件了, 那么恢复后, 事件还在吗?

```javascript
$(function() {
    $("div").click(function() {
        alert("hello world");
    });

    var oDiv = $("div").remove();
    $("body").append(oDiv);
});
```

那 `detach`呢?

```javascript
$(function() {
    $("div").click(function() {
        alert("hello world");
    });

    var oDiv = $("div").detach();
    $("body").append(oDiv);
});
```

## `$()` === `$(document).ready()`

`$()` !== `window.onload`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <img src="https://www.xujunhao.com/hello.jpg" />
    </body>
    <script>
        // window.onload = function() {
        //     alert("hello world");
        // };

        $(function() {
            alert("hello world");
        });
    </script>
</html>
```

`$()`相当于...

```javascript
$(document).ready(function() {
    alert("hello world");
});
```

window.onload, 只执行一次
document.ready, 可以执行很多次
