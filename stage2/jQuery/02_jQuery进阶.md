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
`$('li')[0]` 原生 js 对象
`$('li').eq(0)` jquery 的对象

如果想给第一个 li 设置背景...

```javascript
$("li")[0].style.background = "red";
```

```javascript
$("li")
    .eq(0)
    .css("background", "red");
```

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
jquery 的 outerWidth() 依然有值

`visibility: hidden;` 呢?

offsetWidth ==> 200
jquery 的 outerWidth() 200

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

html() 只获取第一行
text() 获取所有文本

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

html()和 text() 在赋值时, 都是全部

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

不在

```javascript
$(function() {
    $("div").click(function() {
        alert("hello world");
    });

    var oDiv = $("div").remove();
    $("body").append(oDiv);
});
```

那 `detach`呢?(还会保留原来的事件)

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

`window.onload` 会等待外部资源加载完毕在执行 js
`$(document).ready()` ==> html 标签跑完, 就可以执行 js, 不用等待外部资源加载完毕

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

window.onload, 只执行一次, 多个执行最后一个

```javascript
window.onload = function() {
    alert("来啦? 老弟");
};
window.onload = function() {
    alert("又来啦? 老弟");
};
window.onload = function() {
    alert("还来啊? 老弟");
};
window.onload = function() {
    alert("再来啊? 老弟");
};
window.onload = function() {
    alert("滚蛋");
};
```

document.ready, 可以执行很多次

```javascript
$(document).ready(function() {
    alert("来啦? 老弟");
});
$(document).ready(function() {
    alert("又来啦? 老弟");
});
$(document).ready(function() {
    alert("还来啊? 老弟");
});
$(document).ready(function() {
    alert("再来啊? 老弟");
});
$(document).ready(function() {
    alert("滚蛋");
});
```

$() ===$(document).ready()

```javascript
$(function() {
    alert("来啦? 老弟");
});
$(function() {
    alert("又来啦? 老弟");
});
$(function() {
    alert("双来啊? 老弟");
});
$(function() {
    alert("叒来啊? 老弟");
});
$(function() {
    alert("叕来啊? 老弟");
});
$(function() {
    alert("滚蛋");
});
```

## `parents()` `closest()`

父亲们???

先看看 `parent`...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>

        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
            #div2 {
                width: 100px;
                height: 100px;
                background: yellow;
            }
        </style>
    </head>
    <body>
        <div id="div1"><div id="div2"></div></div>
    </body>

    <script>
        $(function() {
            $("#div2")
                .parent()
                .css("background", "yellowgreen");
        });
    </script>
</html>
```

parents? 父亲们? 不应该只有一个父亲吗?
再试试`parents()`...

祖先的意思

```javascript
$(function() {
    $("#div2")
        .parents()
        .css("background", "yellowgreen");
});
```

注意`parents`和`parent`的区别

-   `parent()` 是获取父级节点
-   `parents()` 是获取所有祖先节点

如果`parents()`后接`html()`会是什么?

```javascript
$(function() {
    console.log(
        $("#div2")
            .parents()
            .html()
    );
});
```

获取了 div1 的内容

`parents()`到底是什么?

```javascript
$(function() {
    console.log($("#div2").parents());
});
```

`parents()`可以有参数吗?

表示筛选...

```javascript
$(function() {
    console.log(
        $("#div2")
            .parents("body")
            .html()
    );
});
```

如果没有就 undefined

`closest()`和`parents()`有什么区别?

closest? 最近?

当`closest()`有参数时...

筛选最近的一个祖宗

```javascript
$(function() {
    console.log(
        $("#div2")
            .closest("body")
            .html()
    );
});
```

既然是最近, 那么多个标签同一个 class 呢? 还是最近

如果`closest()`没有参数呢...会 undefined, 所以一定要有参数

```javascript
$(function() {
    console.log(
        $("#div2")
            .closest()
            .html()
    );
});
```

打印一下, `closeets()`到底是什么?

```javascript
$(function() {
    console.log($("#div2").closest());
});
```

祖先可以包括元素自己吗?

往上找, 找最近的, 当然可以找到自己, parents 不行

```javascript
$(function() {
    console.log(
        $("#div2")
            .closest("#div2")
            .html()
    );
});
```

总结一下

-   `closest()` 必须有参数
-   `parents()` 可以没有参数, 表示所有祖先
-   `closest()` 表示祖先, 可以包括元素本身, 因为是一级一级往上找, 找最近
-   `parents()` 也表示祖先, ,但是不包括元素本身
-   `closest()` 只选一个, 最近的
-   `parents()` 使用筛选条件, 可以筛出来很多个

```javascript
$(function() {
    console.log($("#div2").parents(".div0"));
});
```

## `sibling()` 和 `siblings()`

`sibling()` 压根儿, 没有这个方法
`siblings()` 表示所有兄弟节点, 参数表筛选

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>div</div>
        <span>span</span>
        <h2>h2</h2>
        <h3>h3</h3>
        <p>p</p>
    </body>
    <script>
        $("span")
            .siblings()
            .css("background", "red");
    </script>
</html>
```

```javascript
$("span")
    .siblings("h3")
    .css("background", "red");
```

参数表示筛选, 可以筛选出很多个

例子中的`siblings`有多少个?

```javascript
console.log($("span").siblings());
```

注意 script...

尝试取出脚本内容

```javascript
console.log(
    $("span")
        .siblings("script")
        .html()
);
```

## `nextAll()` `prevAll()`

回忆一下 `next()`和`prev()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>div</div>
        <span>span</span>
        <h2>h2</h2>
        <h3>h3</h3>
        <p>p</p>
    </body>
    <script>
        console.log(
            $("span")
                .next()
                .css("background", "red")
        );
    </script>
</html>
```

```javascript
console.log(
    $("span")
        .next()
        .next()
        .next()
        .css("background", "red")
);
```

```javascript
console.log(
    $("span")
        .prev()
        .css("background", "red")
);
```

`nextAll()`返回所有的弟弟

```javascript
$("span")
    .nextAll()
    .css("background", "red");
```

可以接收参数吗?

```javascript
$("span")
    .nextAll("p")
    .css("background", "red");
```

`prevAll()`返回所有的哥哥

```javascript
$("span")
    .prevAll()
    .css("background", "red");
```

可以接收参数吗?

```javascript
$("span")
    .prevAll("p")
    .css("background", "red");
```

## `parentsUntil()` `nextUntil()` `prevUntil()`

`until`表示截止, 直到...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>div</div>
        <span>span</span>
        <h2>h2</h2>
        <h3>h3</h3>
        <p>p</p>
    </body>
    <script>
        $("p")
            .prevUntil("span")
            .css("background", "red");
    </script>
</html>
```

请思考一下, 如果`preUntil('span')`, 请问包括`span`吗?

不包括

如果不加参数呢? 和 prevAll 一样

```javascript
$("p")
    .prevUntil("span")
    .css("background", "red");
```

`nextUntil()` 和 `prevUntil()` 同理吗?

```javascript
$("div")
    .nextUntil("p")
    .css("background", "red");
```

```javascript
$("div")
    .nextUntil()
    .css("background", "red");
```

`parentsUntil()`同理吗?

是的

1. 不传参数, 是不是全选
2. 传了参数, 是否包含该参数
3. 能否传自己? 如果传自己, 一定找不到, 跟不传参一样

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
        <style>
            #div1 {
                width: 500px;
                height: 500px;
                border: 1px solid red;
            }
            #div2 {
                width: 400px;
                height: 400px;
                border: 1px solid yellow;
            }
            #div3 {
                width: 300px;
                height: 300px;
                border: 1px solid blue;
            }
            #div4 {
                width: 200px;
                height: 200px;
                border: 1px solid green;
            }
            #div5 {
                width: 100px;
                height: 100px;
                border: 1px solid yellowgreen;
            }
        </style>
    </head>
    <body>
        <div id="div1">
            <div id="div2">
                <div id="div3">
                    <div id="div4"><div id="div5"></div></div>
                </div>
            </div>
        </div>
    </body>
    <script>
        $("#div5")
            .parentsUntil("#div3")
            .css("background", "red");
    </script>
</html>
```

## `clone()`

回忆一下原生中的克隆...

看看 jquery 的`clone()`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>div</div>
        <span>span</span>
    </body>
    <script>
        $(function() {
            // $("div").appendTo($("span"));
            $("span")
                .get(0)
                .appendChild($("div").get(0));
        });
    </script>
</html>
```

```javascript
$(function() {
    $("div")
        .clone()
        .appendTo($("span"));
});
```

`clone()`可以接收一个参数, 作用可以复制之前的操作行为

```javascript
$(function() {
    $("div").on("click", function() {
        alert("hello world");
    });

    $("div")
        .clone()
        .appendTo($("span"));
});
```

加 `true` 的话, 可以复制事件

```javascript
$(function() {
    $("div").on("click", function() {
        alert("hello world");
    });

    $("div")
        .clone(true)
        .appendTo($("span"));
});
```

支持多个事件

```javascript
$(function() {
    $("div").on("click mouseover", function() {
        alert("hello world");
    });

    $("div")
        .clone(true)
        .appendTo($("span"));
});
```

1. jquery 模拟的是 js 的深复制, 还是浅复制?

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div id="divFirst">
            <div id="div1"></div>
            <div id="div2"></div>
            <div id="div3"></div>
            <div id="div4"></div>
            <div id="div5"></div>
            <div id="div6"></div>
            <div id="div7"></div>
            <div id="div8"></div>
            <div id="div9"></div>
            <div id="div10"></div>
        </div>
        <div id="divSecond">
            <div id="div1"></div>
            <div id="div2"></div>
            <div id="div3"></div>
            <div id="div4"></div>
            <div id="div5"></div>
            <div id="div6"></div>
            <div id="div7"></div>
            <div id="div8"></div>
            <div id="div9"></div>
            <div id="div10"></div>
        </div>
    </body>
    <script>
        $(function() {
            $("#divFirst")
                .clone()
                .appendTo($("#divSecond"));
        });
    </script>
</html>
```

2. 原生 js 的 onclick 事件, jquery 的`clone(true)`能否复制?

只能复制jquery的事件

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>div</div>
        <span>span</span>
    </body>
    <script>
        $(function() {
            $("div").get(0).onclick = function() {
                alert("hello world");
            };

            $("div")
                .clone(true)
                .appendTo($("span"));
        });
    </script>
</html>
```

1. 原生 js 的 cloneNode(), 能否复制 onclick 事件? no!!!!!!!!!!!

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div id="div1">this is div 1</div>
        <div id="div2">this is div 2</div>
    </body>
    <script>
        $(function() {
            $("#div1").get(0).onclick = function() {
                alert("hello world");
            };

            $("#div2")
                .get(0)
                .appendChild(
                    $("#div1")
                        .get(0)
                        .cloneNode(true)
                );
        });
    </script>
</html>
```

## `wrap()` `wrapAll()` `wrapInner()` `unwrap ==> 解除包装(删除父级)`




wrap ==> 包装

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span1</span>
        <span>this is span2</span>
        <span>this is span3</span>
        <span>this is span4</span>
    </body>
    <script>
        $(function() {
            $("span").wrap("<div>");
        });
    </script>
</html>
```

可以把标签写全吗?

```javascript
$(function() {
    $("span").wrap("<div></div>");
});
```

如果写多个标签呢?

```javascript
$(function() {
    $("span").wrap("<div><div></div></div>");
});
```

如果标签写不全呢?

```javascript
$(function() {
    $("span").wrap("<p></div>");
});
```

wrapAll ==> 整体包装

```javascript
$(function() {
    $("span").wrapAll("<p>");
});
```

如果 span 被隔开了呢?

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span1</span>
        <span>this is span2</span>
        <span>this is span3</span>
        <p>pppp</p>
        <span>this is span4</span>
    </body>
    <script>
        $(function() {
            $("span").wrapAll("<p>");
        });
    </script>
</html>
```

wrapInner ==> 内部包装

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <span>this is span1</span>
        <span>this is span2</span>
        <span>this is span3</span>
        <span>this is span4</span>
    </body>
    <script>
        $(function() {
            $("span").wrapInner("<p>");
        });
    </script>
</html>
```

unwrap ==> 解除包装(删除父级)

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <p><span>this is span1</span></p>
        <p><span>this is span2</span></p>
        <p><span>this is span3</span></p>
        <p><span>this is span4</span></p>
    </body>
    <script>
        $(function() {
            $("span").unwrap();
        });
    </script>
</html>
```

如果传参数呢?

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <p><span>this is span1</span></p>
        </div>
        <div>
            <p><span>this is span2</span></p>
        </div>
        <div>
            <p><span>this is span3</span></p>
        </div>
        <div>
            <p><span>this is span4</span></p>
        </div>
    </body>
    <script>
        $(function() {
            $("span").unwrap("p");
        });
    </script>
</html>
```

如果父级是 body 呢? body删不了

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <div>
            <p><span>this is span1</span></p>
        </div>
        <div>
            <p><span>this is span2</span></p>
        </div>
        <div>
            <p><span>this is span3</span></p>
        </div>
        <div>
            <p><span>this is span4</span></p>
        </div>
    </body>
    <script>
        $(function() {
            $("div").unwrap();
        });
    </script>
</html>
```

## `add()` `slice()`

如果我想把一个元素的背景变红...

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
            $("div").css("background", "red");
        });
    </script>
</html>
```

如果我想让两个元素变红呢?

```javascript
$(function() {
    $("div").css("background", "red");
    $("span").css("background", "red");
});
```

如果我想一行代码搞定呢?

```javascript
$(function() {
    $("div")
        .add("span")
        .css("background", "red");
});
```

add, 组合两个元素, 然后一起操作...

那么`slice`呢? 莫非是传说中的`对象切片`?

传入`起始位置`和`结束位置`即可 不包括结束位置 `[0,4)`

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li 1</li>
            <li>this is li 2</li>
            <li>this is li 3</li>
            <li>this is li 4</li>
            <li>this is li 5</li>
            <li>this is li 6</li>
            <li>this is li 7</li>
            <li>this is li 8</li>
            <li>this is li 9</li>
            <li>this is li 10</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li")
                .slice(0, 4)
                .css("background", "red");
        });
    </script>
</html>
```

只有开始位置呢?

```javascript
$(function() {
    $("li")
        .slice(0)
        .css("background", "red");
});
```

开始结束都没有呢?

```javascript
$(function() {
    $("li")
        .slice()
        .css("background", "red");
});
```

只有结束, 没有开始呢? 报错了, 你个损戳儿...

```javascript
$(function() {
   $("li")
       .slice(,4)
       .css("background", "red");
});
```

结束位置越界了呢? 就是到底

```javascript
$(function() {
    $("li")
        .slice(1, 444)
        .css("background", "red");
});
```

## `serialize()` `serializeArray()`

表单数据串联, 一个串联成字符串, 一个串联成数组

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <form action="index.php">
            <input type="text" name="a" value="1" />
            <input type="text" name="b" value="2" />
            <input type="text" name="c" value="3" />
        </form>
    </body>
    <script>
        $(function() {
            console.log($("form").serialize()); // a=1&b=2&c=3
        });
    </script>
</html>
```

省了很多事情, 如果没有, 会这样写...

```javascript
$(function() {
    console.log($("[name=a]").val());
    console.log($("[name=b]").val());
    console.log($("[name=c]").val());
    console.log($("[name=d]").val());
});
```

循环能省事儿吗?

```javascript
$(function() {
    var arr = [];
    $("input").each(function(key, value) {
        arr.push(
            $("input")
                .eq(key)
                .attr("name")
        );
    });
    $("input").each(function(key, value) {
        var str =
            arr[key] +
            " = " +
            $("input")
                .eq(key)
                .attr("value");
        eval(str);
    });
    console.log(a);
    console.log(b);
    console.log(c);
});
```

更费劲.......

还可以转数组(json 格式)

```javascript
$(function() {
    console.log($("form").serializeArray());
    // [
    //     {
    //         a: "1"
    //     },
    //     {
    //         b: "2"
    //     },
    //     {
    //         c: "3"
    //     }
    // ];
});
```

<!---------------------- 运动篇... ------------------->

## `animate()`

动画, 第一个参数是个对象, 设置运动的终点, 第二个参数时时间, 因为起点(css 已经写好)和终点(第一个参数)已经确定, 所以时间可以决定运动速度

点击变大...

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
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                $(this).animate(
                    {
                        width: "400px",
                        height: "400px"
                    },
                    1000
                );
            });
        });
    </script>
</html>
```

如果宽高写成数字呢?

```javascript
$(function() {
    $("div").click(function() {
        $(this).animate(
            {
                width: 400,
                height: 400
            },
            1000
        );
    });
});
```

还有没有第三个参数?

运动类型 默认 swing 慢快慢, linear 匀速

对比一下

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
        <div class="div1"></div>
        <br />
        <div class="div2"></div>
    </body>
    <script>
        $(function() {
            $(".div1").click(function() {
                $(".div1").animate(
                    {
                        width: 400,
                        height: 400
                    },
                    10000,
                    "swing"
                );
                $(".div2").animate(
                    {
                        width: 400,
                        height: 400
                    },
                    10000,
                    "linear"
                );
            });
        });
    </script>
</html>
```

还有没有第四个参数?

回调函数

```javascript
$(function() {
    $("div").click(function() {
        $(this).animate(
            {
                width: 400,
                height: 400
            },
            1000,
            function() {
                alert("完事...");
            }
        );
    });
});
```

刚才是变大,宽和高同时增加, 可不可以先变宽再变高呢?

```javascript
$(function() {
    $("div").click(function() {
        $(this).animate(
            {
                width: 400
            },
            1000,
            function() {
                $(this).animate(
                    {
                        height: 400
                    },
                    1000
                );
            }
        );
    });
});
```

听说 jquery 的链式操作, 强大很啊!

```javascript
$(function() {
    $("div").click(function() {
        $(this)
            .animate({ width: 400 }, 1000)
            .animate({ height: 400 }, 1000);
    });
});
```

## `stop()`

终止运动
让我们给一个`终止按钮`

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
        <input type="button" value="stop" />

        <div></div>
    </body>
    <script>
        $(function() {
            $("div").click(function() {
                $(this)
                    .animate({ width: 400 }, 7000)
                    .animate({ height: 400 }, 7000);
            });
            $("[type=button]").click(function() {
                $("div").stop();
            });
        });
    </script>
</html>
```

注意, `stop()`只能终止当前运动

那要是向全部停止怎么办? 除了点两次...

还记得 jquery 的`clone(true)`

那我们可不可以往`stop()`里传一个`true`?

```javascript
$(function() {
    $("div").click(function() {
        $(this)
            .animate({ width: 400 }, 7000)
            .animate({ height: 400 }, 7000);
    });
    $("[type=button]").click(function() {
        $("div").stop(true);
    });
});
```

还有没有第二个参数呢?

还真有...

```javascript
$("[type=button]").click(function() {
    $("div").stop(true, true);
});
```

作用, 快速到结尾...

但是好像只能`快进`一个

如果想同时快进呢?

```javascript
$("[type=button]").click(function() {
    $("div").finish();
});
```

## `delay()`

延迟???

如果我想 div 先变宽, 歇一会儿, 然后再变高呢?

```javascript
$("div").click(function() {
    $(this)
        .animate({ width: 400 })
        .delay(1000)
        .animate({ height: 400 });
});
```

## `delegate()` `undelegate()`

代理???

事件委托

是干嘛用的?

我们之前给 li 添加点击事件...

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li 1</li>
            <li>this is li 2</li>
            <li>this is li 3</li>
            <li>this is li 4</li>
            <li>this is li 5</li>
            <li>this is li 6</li>
            <li>this is li 7</li>
            <li>this is li 8</li>
            <li>this is li 9</li>
            <li>this is li 10</li>
        </ul>
    </body>
    <script>
        $(function() {
            $("li").on("click", function() {
                $(this).css("background", "red");
            });
        });
    </script>
</html>
```

那我可不可以在 ul 上添加事件呢?

没有问题!!!

```javascript
$(function() {
    $("ul").delegate("li", "click", function() {
        $(this).css("background", "red");
    });
});
```

委托 ul 代理其下的 li 的 onclick 事件

那么其他地方的 li, 可以用吗?

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <ul>
            <li>this is li 1</li>
            <li>this is li 2</li>
            <li>this is li 3</li>
            <li>this is li 4</li>
            <li>this is li 5</li>
            <li>this is li 6</li>
            <li>this is li 7</li>
            <li>this is li 8</li>
            <li>this is li 9</li>
            <li>this is li 10</li>
        </ul>
        <li>this is li 10</li>
    </body>
    <script>
        $(function() {
            $("ul").delegate("li", "click", function() {
                $(this).css("background", "red");
            });
        });
    </script>
</html>
```

区别何在?

1. 把事件加在了 ul 身上, 点击事件, 利用冒泡, 触发 ul 的事件, 所以这也是外面的 li, 不行的原因
2. 省略了循环操作, 只需在 ul 上添加事件即可
3. 新增加的节点, 自动拥有相关事件

`undelegate` 取消事件委托

```javascript
$(function() {
    $("ul").delegate("li", "click", function() {
        $(this).css("background", "red");
        $("ul").undelegate();
    });
});
```

## `trigger()`

扳机???
主动触发
触发已经添加在 jquery 对象上的事件

还是经典的`DCH`(div,click,hello world)

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
            $("div").on("click", function() {
                alert("hello world");
            });
        </script>
    </body>
</html>
```

现在我想, 加载完页面, 立即弹出 hello world, 怎么办?

```javascript
$("div").on("click", function() {
    alert("hello world");
});
$("div").trigger("click");
```

如果是自定义事件呢?

其实 trigger 就是触发自定义事件

```javascript
$("div").on("myFn", function() {
    alert("hello world");
});
$("div").trigger("myFn");
```

如何通过点击来触发自定义事件?

```javascript
$("div").on("myFn", function() {
    alert("hello world");
});
$("div").on("click", function() {
    $("div").trigger("myFn");
});
```

自定义事件如果重名呢?

```javascript
$("div").on("myFn", function() {
    alert("hello world");
});
$("div").on("myFn", function() {
    alert("hello world!!!");
});
$("div").on("click", function() {
    $("div").trigger("myFn");
});
```


