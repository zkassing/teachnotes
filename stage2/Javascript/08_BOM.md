# 作为值的函数

-   因为 ECMAScript 中的函数名本身就是变量，所以函数也可以作为值来使用。
-   不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回

```javascript
function callSomeFunction(someFunction, someArgument) {
    return someFunction(someArgument);
}

function add10(num) {
    return num + 10;
}

console.log(callSomeFunction(add10, 10)); // 20

function getGreeting(userName) {
    return "Hello " + userName + " !!!";
}

console.log(callSomeFunction(getGreeting, "ZhangSan")); // hello ZhangSan
```

## 再谈数组排序`arr.sort`(默认每个元素都会调用`toString()`方法)

### 数字排序 vs 字符串排序

```javascript
var arr = [1, 11, 22, 2, 3, 4];
var arr1 = ["1", "11", "22", "2", "3", "4"];
arr.sort();
console.log(arr);
arr1.sort();
console.log(arr1);

arr.sort(function(a, b) {
    return a - b;
});

console.log(arr);
arr1.sort(function(a, b) {
    return a - b;
});

console.log(arr1);

console.log("123" - "22");
```

### 对象排序

> 函数的返回值, 还是函数

```javascript
function createComparisonFunction(propertyName) {
    return function(object1, object2) {
        var value1 = object1[propertyName];
        var value2 = object2[propertyName];
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            return 0;
        }
    };
}

var data = [
    {
        name: "Mike",
        age: 29
    },
    {
        name: "ZhangSan",
        age: 28
    }
];

data.sort(); // 如果不传参数, 默认每个元素toString(), 然后排序, 对象的toString()返回结果都一样, 所以看起来好像排序没有作用...
console.log(data);
```

## array.sort 接收函数做参数的原理

```javascript
function mySort(fnName) {
    for (var k = 1; k < this.length; k++) {
        for (var j = 0; j < this.length - k; j++) {
            if (fnName(this[j], this[j + 1]) > 0) {
                temp = this[j + 1];
                this[j + 1] = this[j];
                this[j] = temp;
            }
        }
    }
    return this;
}
var arr = [5, 4, 3, 2, 1, 23];
arr.__proto__.mySort = mySort;
console.log(arr);

function fnName(a, b) {
    return a - b;
}

console.log(arr.mySort(fnName));
console.log(arr);
```

# 聊聊 css 函数

## css 函数如何使用?(函数重载)

> css(oDiv, 'width') 获取样式
> css(oDiv, 'width', '200px') 设置样式

第一个版本

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1" style="width:200px;height: 200px;background: red;"></div>
    </body>
    <script>
        function css() {
            if (arguments.length === 2) {
                return arguments[0].style[arguments[1]];
            } else {
                arguments[0].style[arguments[1]] = arguments[2];
            }
        }
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            // alert(css(oDiv, "width"));
            css(oDiv, "background", "green");
        };
    </script>
</html>
```

优化函数参数之后的版本

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1" style="width:200px;height: 200px;background: red;"></div>
    </body>
    <script>
        function css(obj, name, value) {
            if (arguments.length === 2) {
                return obj.style[name];
            } else {
                obj.style[name] = value;
            }
        }
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            // alert(css(oDiv, "width"));
            css(oDiv, "background", "green");
        };
    </script>
</html>
```

函数参数的默认值问题

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div
            id="div1"
            style="width:200px;height: 200px;background: red;font-size: 20px"
        ></div>
    </body>
    <script>
        function css(obj, name, value="") {
            console.log(value); // 严格模式下, 会报错 expected token =

            if (arguments.length === 2) {
                return obj.style[name];
            }
            if (arguments.length === 3) {
                obj.style[name] = value;
            }
        }
        window.onload = function() {
            var oDiv = document.getElementById("div1");

            // console.log(css(oDiv, "width"));
            console.log(css(oDiv, "background"));
        };
    </script>
</html>
```

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div
            id="div1"
            style="width:200px;height: 200px;background: red;font-size: 20px"
        ></div>
    </body>
    <script>
        function css(obj, name, value) {
            value = value || ""; // 参数默认值的推荐写法
            console.log(value);

            if (arguments.length === 2) {
                return obj.style[name];
            }
            if (arguments.length === 3) {
                obj.style[name] = value;
            }
        }
        window.onload = function() {
            var oDiv = document.getElementById("div1");

            // console.log(css(oDiv, "width"));
            console.log(css(oDiv, "background"));
        };
    </script>
</html>
```

# 获取对象样式(非行间)

## 先复习一下获取行间样式

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1" style="width:200px;height: 200px;background: red;"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            alert(oDiv.style.width);
        };
    </script>
</html>
```

**当样式写在样式表里...**

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            alert(oDiv.style.width);
        };
    </script>
</html>
```

**获取不到怎么办?**

> currentStyle

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            alert(oDiv.currentStyle.width);
        };
    </script>
</html>
```

#### js 第二定律

> 但凡好功能, 一定不兼容(currentStyle 只支持 IE)

没关系, 还有一个函数可以用(`getComputedStyle`)

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            // alert(oDiv.currentStyle.width);
            alert(getComputedStyle(oDiv).width);
        };
    </script>
</html>
```

### 解决兼容性问题

##### 什么叫解决兼容性问题?

> 代码, 在所有浏览器都可以正常运行
> 找到不同浏览器之间的不同, 根据不同浏览器, 写不同的代码

_可以两个写法都用吗?_

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");
            alert(oDiv.currentStyle.width);
            alert(getComputedStyle(oDiv).width);
        };
    </script>
</html>
```

## 到底如何解决兼容性

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");

            if (oDiv.currentStyle) {
                alert(oDiv.currentStyle.width);
            } else {
                alert(getComputedStyle(oDiv).width);
            }
        };
    </script>
</html>
```

还有优化的可能

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            var oDiv = document.getElementById("div1");

            var objStyle = oDiv.currentStyle || getComputedStyle(oDiv);
            alert(objStyle.width);

        };
    </script>
</html>
```

### 右滑解决方案(封装一个自己的函数)

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        function getStyle(obj, name) {
            if (obj.currentStyle) {
                return obj.currentStyle[name];
            } else {
                return getComputedStyle(obj)[name];
            }
        }

        window.onload = function() {
            var oDiv = document.getElementById("div1");
            console.log(getStyle(oDiv, "width"));
        };
    </script>
</html>
```

#### background 和 background-color 的问题

> 只能获取单一样式, 不能获取复合样式(IE)

解决方案

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: yellow;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        function getStyle(obj, name) {
            if (name === "background") {
                name = "backgroundColor";
            }
            if (obj.currentStyle) {
                return obj.currentStyle[name];
            } else {
                return getComputedStyle(obj)[name];
            }
        }

        window.onload = function() {
            var oDiv = document.getElementById("div1");
            alert(getStyle(oDiv, "background"));
            console.log(getStyle(oDiv, "background"));
        };
    </script>
</html>
```

# window 对象

在浏览器中， window 对象有双重角色，
它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。

## 全局作用域

> 由于 window 对象同时扮演着 ECMAScript 中 Global 对象的角色，因此所有在全局作用域中声明的变量、函数都会变成 window 对象的属性和方法

```javascript
var age = 29;
function sayAge() {
    alert(this.age);
}
alert(window.age);
sayAge();
window.sayAge();
```

## 系统对话框

> 浏览器通过 alert() 、 confirm() 和 prompt() 方法可以调用系统对话框向用户显示消息。

### `alert()`

### `confirm()`

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <script>
            if (confirm("你是一个帅哥吗?")) {
                alert("你居然点了确定, 臭不要脸! ");
            } else {
                alert("做人要有自信啊...");
            }
        </script>
    </body>
</html>
```

### `prompt()`

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <script>
            var result = prompt("帅哥, 处对象不?", "请输入你的回答...");
            if (result !== null) {
                alert("你居然回答'" + result + "'?! 就喜欢你强势的样子...");
            }
        </script>
    </body>
</html>
```

# location 对象

location 是最有用的 BOM 对象之一，它提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能。
location 对象是很特别的一个对象，因为它既是 window 对象的属性，也是 document 对象的属性；
换句话说， window.location 和 document.location 引用的是同一个对象。
location 对象的用处不只表现在它保存着当前文档的信息，还表现在它将 URL 解析为独立的片段，让开发人员可以通过不同的属性访问这些片段

`hash`

> eg: "#contents"
> 返回 URL 中的 hash（#号后跟零或多个字符），如果 URL 中不包含散列，则返回空字符串

`host`

> eg: "www.baidu.com:80"
> 返回服务器名称和端口号（如果有）

`hostname`

> eg: "www.baidu.com"
> 返回不带端口号的服务器名称

`href`

> eg: "http:/www.baidu.com"
> 返回当前加载页面的完整 URL。而 location 对象的 toString()方法也返回这个值

`pathname`

> eg: "/WileyCDA/"
> 返回 URL 中的目录和（或）文件名

`port`

> eg: "8080"
> 返回 URL 中指定的端口号。如果 URL 中不包含端口号，则这个属性返回空字符串

`protocol`

> eg: "http:"
> 返回页面使用的协议。通常是 http:或 https:

`search`

> eg: "?q=javascript"
> 返回 URL 的查询字符串。这个字符串以问号开头

## 页面跳转

使用 a 标签

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <a href="https://www.baidu.com">百度一下</a>
</body>
</html>
```

点击按钮跳转呢?

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <a href="https://www.baidu.com">
            <input type="button" value="百度一下" />
        </a>
    </body>
</html>
```

js 的三种跳转方式

```javascript
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <script>
            location.assign("https://www.baidu.com");
            window.location = "https://www.sina.com";
            location.href = "https://www.sohu.com";
        </script>
    </body>
</html>
```

# history 对象

history 对象保存着用户上网的历史记录，从窗口被打开的那一刻算起。因为 history 是 window 对象的属性，因此每个浏览器窗口、每个标签页，都有自己的 history 对象与特定的 window 对象关联。
使用 go() 方法可以在用户的历史记录中任意跳转，可以向后也可以向前。这个方法接受一个参数， 表示向后或向前跳转的页面数的一个整数值。负数表示向后跳转（类似于单击浏览器的“后退”按钮）， 正数表示向前跳转（类似于单击浏览器的“前进”按钮）。

```javascript
//后退一页
history.go(-1);
//前进一页
history.go(1);
//前进两页
history.go(2);
```

还可以使用两个简写方法 back() 和 forward() 来代替 go() 。顾名思义，这两个方法可以模仿浏览器的“后退”和“前进”按钮。

```javascript
//后退一页
history.back();
//前进一页
history.forward();
```

history 对象还有一个 length 属性，保存着历史记录的数量

```javascript
history.length;
```
