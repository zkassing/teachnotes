# DOM 概述

## DOM

1. DOM 是 JavaScript 操作网页的接口，全称为“文档对象模型”（Document Object Model）。
1. 它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。
1. 浏览器会根据 DOM 模型，将结构化文档（比如 HTML 和 XML）解析成一系列的节点，再由这些节点组成一个树状结构（DOM Tree）。
1. 所有的节点和最终的树状结构，都有规范的对外接口。
1. DOM 操作是 JavaScript 最常见的任务，离开了 DOM，JavaScript 就无法控制网页

## 节点

> DOM 的最小组成单位叫做节点（node）。
> 文档的树形结构（DOM 树），就是由各种不同类型的节点组成。
> 每个节点可以看作是文档树的一片叶子。

节点的类型有七种。

1. `Document`：整个文档树的顶层节点
1. `Element`：网页的各种 HTML 标签（比如<body>、<a>等）
1. `Attribute`：网页元素的属性（比如 class="right"）
1. `Text`：标签之间或标签包含的文本
1. `Comment`：注释

> 浏览器提供一个原生的节点对象 Node，
> 上面这七种节点都继承了 Node，因此具有一些共同的属性和方法。

## 节点树

> 一个文档的所有节点，按照所在的层级，可以抽象成一种树状结构。这种树状结构就是 DOM 树。
> 它有一个顶层节点，下一层都是顶层节点的子节点，然后子节点又有自己的子节点，就这样层层衍生出一个金字塔结构，倒过来就像一棵树。

_浏览器原生提供 document 节点，代表整个文档。_

> 控制台输出 document, 会是什么?

文档的第一层只有一个节点，就是 HTML 网页的第一个标签<html>
它构成了树结构的根节点（root node），其他 HTML 标签节点都是它的下级节点。

除了根节点，其他节点都有三种层级关系。

1. 父节点关系（`parentNode`）：直接的那个上级节点
1. 子节点关系（`childNodes`）：直接的下级节点
1. 同级节点关系（`sibling`）：拥有同一个父节点的节点

DOM 提供操作接口，用来获取这三种关系的节点。
子节点接口包括 `firstChild`（第一个子节点）和 `lastChild`（最后一个子节点）等属性，
同级节点接口包括 `nextSibling`（紧邻在后的那个同级节点）和 `previousSibling`（紧邻在前的那个同级节点）属性。

# Node 接口

## 属性

### Node.prototype.nodeType

> nodeType 属性返回一个整数值，表示节点的类型。

_document.nodeType 是多少?_

Node 对象定义了几个常量，对应这些类型值。

```javascript
document.nodeType === Node.DOCUMENT_NODE; // true
```

不同节点的 nodeType 属性值和对应的常量如下。

-   文档节点（`document`）：9，对应常量 `Node.DOCUMENT_NODE`
-   元素节点（`element`）：1，对应常量 `Node.ELEMENT_NODE`
-   属性节点（`attr`）：2，对应常量 `Node.ATTRIBUTE_NODE`
-   文本节点（`text`）：3，对应常量 `Node.TEXT_NODE`
-   文档片断节点（`DocumentFragment`）：11，对应常量 `Node.DOCUMENT_FRAGMENT_NODE`
-   文档类型节点（`DocumentType`）：10，对应常量 `Node.DOCUMENT_TYPE_NODE`
-   注释节点（`Comment`）：8，对应常量 `Node.COMMENT_NODE`

确定节点类型时，使用 nodeType 属性是常用方法。

```javascript
var node = document.documentElement.firstChild;
if (node.nodeType === Node.ELEMENT_NODE) {
    console.log("该节点是元素节点");
}
```

### Node.prototype.nodeName

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"></div>
        <!-- 如果改成别的... -->
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.nodeName ↓↓↓↓↓↓");
            console.log(oDiv.nodeName);
        };
    </script>
</html>
```

> `nodeName`属性返回节点的名称。

不同节点的 nodeName 属性值如下。

1. 文档节点（`document`）：#document
1. 元素节点（`element`）：大写的标签名
1. 属性节点（`attr`）：属性的名称
1. 文本节点（`text`）：#text
1. 文档片断节点（`DocumentFragment`）：#document-fragment
1. 文档类型节点（`DocumentType`）：文档的类型
1. 注释节点（`Comment`）：#comment

### Node.prototype.nodeValue

> `nodeValue` 属性返回一个字符串，表示当前节点本身的文本值，该属性可读写。

只有文本节点（text）、注释节点（comment）和属性节点（attr）有文本值，因此这三类节点的 nodeValue 可以返回结果，其他类型的节点一律返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <hello id="div1"></hello>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.nodeValue ↓↓↓↓↓↓");
            console.log(oDiv.nodeValue); // null
        };
    </script>
</html>
```

文本节点例子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <hello id="div1">hello world</hello>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild.nodeValue ↓↓↓↓↓↓");
            oDiv.firstChild.nodeValue = "hello world !!!!!!!!";
            console.log(oDiv.firstChild.nodeValue);
        };
    </script>
</html>
```

注释节点的例子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            div {
                width: 200px;
                height: 200px;
                background: red;
            }
        </style>
    </head>
    <body>
        <div id="div1"><!-- hello world --></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild.nodeValue ↓↓↓↓↓↓");
            oDiv.firstChild.nodeValue = "hello world !!!!!!!!";
            console.log(oDiv.firstChild.nodeValue);
        };
    </script>
</html>
```

属性节点的例子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            .div1 {
                width: 200px;
                height: 200px;
                background: red;
            }
            .div2 {
                width: 300px;
                height: 300px;
                background: green;
            }
        </style>
    </head>
    <body>
        <div id="div1" class="div1"></div>
    </body>
    <script>
        window.onload = function() {
            console.log(
                '↓↓↓↓↓↓ document.getElementById("div1").getAttributeNode("class").nodeValue ↓↓↓↓↓↓'
            );
            console.log(
                document.getElementById("div1").getAttributeNode("class")
                    .nodeValue
            );
            document
                .getElementById("div1")
                .getAttributeNode("class").nodeValue = "div2";
        };
    </script>
</html>
```

同样的，也只有这三类节点可以设置 nodeValue 属性的值，其他类型的节点设置无效。

无效的例子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <hello id="div1"></hello>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.nodeValue ↓↓↓↓↓↓");
            console.log(oDiv.nodeValue); // null
            oDiv.nodeValue = "hello";
            console.log(oDiv.nodeValue);
        };
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
    </head>
    <body>
        <div id="d1">hello world</div>
        <script>
            window.onload = function() {
                var div = document.getElementById("d1");
                div.nodeValue; // null
                console.log("↓↓↓↓↓↓ div.nodeValue ↓↓↓↓↓↓");
                console.log(div.nodeValue);
                div.firstChild.nodeValue; // "hello world"
                console.log("↓↓↓↓↓↓ div.firstChild.nodeValue ↓↓↓↓↓↓");
                console.log(div.firstChild.nodeValue);
                div.firstChild.nodeValue = "hello world!!!!!"; // "hello world"
                console.log("↓↓↓↓↓↓ div.firstChild.nodeValue ↓↓↓↓↓↓");
                console.log(div.firstChild.nodeValue);
                div.nodeValue = "haha";
            };
        </script>
    </body>
</html>
```

_上面代码中，div 是元素节点，nodeValue 属性返回 null。div.firstChild 是文本节点，所以可以返回文本值。_

### Node.prototype.textContent

> `textContent`属性返回当前节点和它的所有后代节点的文本内容。

_换行也会捕捉到_

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            this is
            <span>some</span>
            text
        </div>
    </body>
    <script>
        window.onload = function() {
            console.log(
                '↓↓↓↓↓↓ document.getElementById("div1").textContent ↓↓↓↓↓↓'
            );
            console.log(document.getElementById("div1").textContent);
        };
    </script>
</html>
```

该属性是可读写的，设置该属性的值，会用一个新的文本节点，替换所有原来的子节点。
它还有一个好处，就是自动对 HTML 标签转义。这很适合用于用户提供的内容。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            this is
            <span>some</span>
            text
        </div>
    </body>
    <script>
        window.onload = function() {
            document.getElementById("div1").textContent = "hello world!";
            document.getElementById("div1").textContent =
                "<h1>hello world!</h1>";
        };
    </script>
</html>
```

对于文本节点（text）、注释节点（comment）和属性节点（attr），textContent 属性的值与 nodeValue 属性相同。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            this is
            <span>some</span>
            text
        </div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild.nodeValue ↓↓↓↓↓↓");
            console.log(oDiv.firstChild.nodeValue);
            console.log("↓↓↓↓↓↓ oDiv.firstChild.textContent ↓↓↓↓↓↓");
            console.log(oDiv.firstChild.textContent);
        };
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
    </head>
    <body>
        <div id="div1">
            <!-- this is -->
            <span>some</span>
            text
        </div>
    </body>
    <script>
        // 看看注释节点
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild.nodeValue ↓↓↓↓↓↓");
            console.log(oDiv.firstChild.nodeValue);
            console.log("↓↓↓↓↓↓ oDiv.firstChild.textContent ↓↓↓↓↓↓");
            console.log(oDiv.firstChild.textContent);
        };
    </script>
</html>
```

属性节点的例子

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1" class="div1">
            this is
            <span>some</span>
            text
        </div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log(oDiv.getAttributeNode("class").nodeValue);
            console.log(oDiv.getAttributeNode("class").textContent);
        };
    </script>
</html>
```

对于其他类型的节点，该属性会将每个子节点（不包括注释节点）的内容连接在一起返回。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <!-- this is -->
            <span>some</span>
            text
        </div>
    </body>
    <script>
        // 不包括注释
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.textContent ↓↓↓↓↓↓");
            console.log(oDiv.textContent);
        };
    </script>
</html>
```

如果一个节点没有子节点，则返回空字符串。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.textContent ↓↓↓↓↓↓");
            console.log(oDiv.textContent);
            console.log("↓↓↓↓↓↓ typeof(oDiv.textContent) ↓↓↓↓↓↓");
            console.log(typeof oDiv.textContent);
        };
    </script>
</html>
```

文档节点（document）和文档类型节点（doctype）的 textContent 属性为 null。

```
document.firstChild.textContent
null
document.textContent
null
```

如果要读取整个文档的内容，可以使用 document.documentElement.textContent。

### Node.prototype.baseURI

`baseURI`属性返回一个字符串，表示当前网页的绝对路径。浏览器根据这个属性，计算网页上的相对路径的 URL。
该属性为只读。

```
// 当前网页的网址为
// http://www.example.com/index.html
document.baseURI
// "http://www.example.com/index.html"
```

如果无法读到网页的 URL，baseURI 属性返回 null。

该属性的值一般由当前网址的 URL（即 window.location 属性）决定
但是可以使用 HTML 的<base>标签，改变该属性的值。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <base href="http://www.xujunhao.com" />
        <base target="_blank" />
        <title>Document</title>
    </head>
    <body></body>
    <script>
        window.onload = function() {
            console.log(document.baseURI);
        };
    </script>
</html>
```

设置了以后，baseURI 属性就返回<base>标签设置的值。

### Node.prototype.ownerDocument

`Node.ownerDocument`属性返回当前节点所在的顶层文档对象，即 document 对象。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.ownerDocument ↓↓↓↓↓↓");
            console.log(oDiv.ownerDocument);
        };
    </script>
</html>
```

document 对象本身的 `ownerDocument` 属性，返回 null。

### Node.prototype.nextSibling

`Node.nextSibling` 属性返回紧跟在当前节点后面的第一个同级节点。
如果当前节点后面没有同级节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="d1">hello</div>
        <div id="d2">world</div>
        <script>
            window.onload = function() {
                var div1 = document.getElementById("d1");
                var div2 = document.getElementById("d2");
                console.log(div1.nextSibling === div2);
            };
        </script>
    </body>
</html>
```

注意，该属性还包括文本节点和注释节点（<!-- comment -->）。
因此如果当前节点后面有空格，该属性会返回一个文本节点，内容为空格。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="d1">hello</div>
        <!-- hello world -->
        <div id="d2">world</div>
        <script>
            window.onload = function() {
                console.log(
                    '↓↓↓↓↓↓ document.getElementById("d1").nextSibling.nextSibling ↓↓↓↓↓↓'
                );
                console.log(
                    document.getElementById("d1").nextSibling.nextSibling
                );
            };
        </script>
    </body>
</html>
```

nextSibling 属性可以用来遍历所有子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            hello
            <!-- hello world -->
            <div id="div2">world</div>
        </div>
        <script>
            window.onload = function() {
                var oDiv = document.getElementById("div1").firstChild;
                while (oDiv !== null) {
                    console.log(oDiv.nodeName);
                    oDiv = oDiv.nextSibling;
                }
            };
        </script>
    </body>
</html>
```

上面代码遍历 div1 节点的所有子节点

### Node.prototype.previousSibling

`previousSibling` 属性返回当前节点前面的、距离最近的一个同级节点。
如果当前节点前面没有同级节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="d1">hello</div>
        <div id="d2">world</div>
        <script>
            window.onload = function() {
                var div1 = document.getElementById("d1");
                var div2 = document.getElementById("d2");
                console.log(div2.previousSibling === div1);
            };
        </script>
    </body>
</html>
```

上面代码中，d2.previousSibling 就是 d2 前面的同级节点 d1。

注意，该属性还包括文本节点和注释节点。
因此如果当前节点前面有空格，该属性会返回一个文本节点，内容为空格。

### Node.prototype.parentNode

`parentNode` 属性返回当前节点的父节点。
对于一个节点来说，它的父节点只可能是三种类型：

1. 元素节点（element）
2. 文档节点（document）
3. 文档片段节点（documentfragment）。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="d1">hello</div>
        <div id="d2">world</div>
        <script>
            window.onload = function() {
                var div1 = document.getElementById("d1");
                var div2 = document.getElementById("d2");
                console.log(div1.parentNode.nodeType);
            };
        </script>
    </body>
</html>
```

关于 documentfragment

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>菜鸟教程(runoob.com)</title>
    </head>
    <body>
        <ul>
            <li>Coffee</li>
            <li>Tea</li>
        </ul>
        <p id="demo">
            单击按钮更改列表项,使用createDocumentFragment方法,然后在列表的最后一个孩子添加列表项。
        </p>
        <button onclick="myFunction()">点我</button>
        <script>
            function myFunction() {
                var d = document.createDocumentFragment();
                d.appendChild(document.getElementsByTagName("LI")[0]);
                d.childNodes[0].childNodes[0].nodeValue = "Milk";
                document.getElementsByTagName("UL")[0].appendChild(d);
            }
        </script>
    </body>
</html>
```

文档节点（document）和文档片段节点（documentfragment）的父节点都是 null。

### Node.prototype.parentElement

`parentElement` 属性返回当前节点的父元素节点。
如果当前节点没有父节点，或者父节点类型不是元素节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"><span id="span1"></span></div>
    </body>
    <script>
        window.onload = function() {
            oSpan = document.getElementById("span1");
            console.log("↓↓↓↓↓↓ oSpan.parentNode ↓↓↓↓↓↓");
            console.log(oSpan.parentNode);
            console.log("↓↓↓↓↓↓ oSpan.parentNode.parentNode ↓↓↓↓↓↓");
            console.log(oSpan.parentNode.parentNode);
            console.log("↓↓↓↓↓↓ oSpan.parentNode.parentNode.parentNode ↓↓↓↓↓↓");
            console.log(oSpan.parentNode.parentNode.parentNode);
            console.log(
                "↓↓↓↓↓↓ oSpan.parentNode.parentNode.parentNode.parentNode ↓↓↓↓↓↓"
            );
            console.log(oSpan.parentNode.parentNode.parentNode.parentNode);
            console.log(
                "↓↓↓↓↓↓ oSpan.parentNode.parentNode.parentNode.parentNode.parentNode ↓↓↓↓↓↓"
            );
            console.log(
                oSpan.parentNode.parentNode.parentNode.parentNode.parentNode
            );
            /***********************************************************************************/
            console.log("↓↓↓↓↓↓ oSpan.parentElement ↓↓↓↓↓↓");
            console.log(oSpan.parentElement);
            console.log("↓↓↓↓↓↓ oSpan.parentElement.parentElement ↓↓↓↓↓↓");
            console.log(oSpan.parentElement.parentElement);
            console.log(
                "↓↓↓↓↓↓ oSpan.parentElement.parentElement.parentElement ↓↓↓↓↓↓"
            );
            console.log(oSpan.parentElement.parentElement.parentElement);
            console.log(
                "↓↓↓↓↓↓ oSpan.parentElement.parentElement.parentElement.parentElement ↓↓↓↓↓↓"
            );
            console.log(
                oSpan.parentElement.parentElement.parentElement.parentElement
            );
            console.log(
                "↓↓↓↓↓↓ oSpan.parentElement.parentElement.parentElement.parentElement.parentElement ↓↓↓↓↓↓"
            );
            console.log(
                oSpan.parentElement.parentElement.parentElement.parentElement
                    .parentElement
            );
        };
    </script>
</html>
```

由于父节点只可能是三种类型：

1. 元素节点
2. 文档节点（document）
3. 文档片段节点（documentfragment）。

_`parentElement` 属性相当于把后两种父节点都排除了。_

### Node.prototype.firstChild，Node.prototype.lastChild

`firstChild` 属性返回当前节点的第一个子节点，如果当前节点没有子节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild ↓↓↓↓↓↓");
            console.log(oDiv.firstChild);
        };
    </script>
</html>
```

注意，firstChild 返回的除了元素节点，还可能是文本节点或注释节点。

lastChild 属性返回当前节点的最后一个子节点，如果当前节点没有子节点，则返回 null。用法与 firstChild 属性相同。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"><span>span1</span></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log("↓↓↓↓↓↓ oDiv.firstChild ↓↓↓↓↓↓");
            console.log(oDiv.firstChild);
            console.log("↓↓↓↓↓↓ oDiv.lastChild ↓↓↓↓↓↓");
            console.log(oDiv.lastChild);
        };
    </script>
</html>
```

### Node.prototype.childNodes

`childNodes` 属性返回一个类似数组的对象（NodeList 集合），成员包括当前节点的所有子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </body>
    <script>
        window.onload = function() {
            var children = document.querySelector("ul").childNodes;
            console.log("↓↓↓↓↓↓ children.length ↓↓↓↓↓↓");
            console.log(children.length);
            console.log("↓↓↓↓↓↓ children ↓↓↓↓↓↓");
            console.log(children);
        };
    </script>
</html>
```

上面代码中，children 就是 ul 元素的所有子节点。

使用该属性，可以遍历某个节点的所有子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </body>
    <script>
        window.onload = function() {
            var children = document.querySelector("ul").childNodes;
            console.log("↓↓↓↓↓↓ children.length ↓↓↓↓↓↓");
            console.log(children.length);
            console.log("↓↓↓↓↓↓ children ↓↓↓↓↓↓");
            console.log(children);
            for (var i = 0; i < children.length; i++) {
                console.log("↓↓↓↓↓↓ children[i] ↓↓↓↓↓↓");
                console.log(children[i]);
            }
        };
    </script>
</html>
```

文档节点（document）就有两个子节点：文档类型节点（docType）和 HTML 根元素节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </body>
    <script>
        window.onload = function() {
            var children = document.childNodes;
            for (var i = 0; i < children.length; i++) {
                console.log(children[i].nodeType);
            }
        };
    </script>
</html>
```

上面代码中，文档节点的第一个子节点的类型是 10（即文档类型节点），第二个子节点的类型是 1（即元素节点）。

注意，除了元素节点，childNodes 属性的返回值还包括文本节点和注释节点。
如果当前节点不包括任何子节点，则返回一个空的 NodeList 集合。

### Node.prototype.isConnected

`isConnected` 属性返回一个布尔值，表示当前节点是否在文档之中。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"><span>span1</span></div>
    </body>
    <script>
        window.onload = function() {
            var test = document.createElement("p");
            console.log("↓↓↓↓↓↓ test.isConnected ↓↓↓↓↓↓");
            console.log(test.isConnected);
            document.body.appendChild(test);
            console.log("↓↓↓↓↓↓ test.isConnected ↓↓↓↓↓↓");
            console.log(test.isConnected);
        };
    </script>
</html>
```

上面代码中，test 节点是脚本生成的节点，没有插入文档之前，isConnected 属性返回 false，插入之后返回 true。


# 方法

## Node.prototype.appendChild()

`appendChild` 方法接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点。
`appendChild` 返回新增的节点

```html
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
            window.onload = function() {
                var p = document.createElement("p");
                var returnedNode = document.body.appendChild(p);
                console.log(returnedNode === p);
                console.log(document.body.lastChild === p);
            };
        </script>
    </body>
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
    </head>
    <body>
        <script>
            window.onload = function() {
                var p = document.createElement("p");
                console.log("↓↓↓↓↓↓ document.body.appendChild(p) ↓↓↓↓↓↓");
                console.log(document.body.appendChild(p));
                console.log(document.body.lastChild);
            };
        </script>
    </body>
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
    </head>
    <body>
        <script>
            window.onload = function() {
                var element = document
                    .createElement("div")
                    .appendChild(document.createElement("b"));
                console.log("↓↓↓↓↓↓ element ↓↓↓↓↓↓");
                console.log(element);
            };
        </script>
    </body>
</html>
```

如果参数节点是 DOM 已经存在的节点，appendChild 方法会将其从原来的位置，移动到新位置。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li>this is li0</li>
            <li>this is li1</li>
            <li>this is li2</li>
            <li>this is li3</li>
            <li>this is li4</li>
            <li>this is li5</li>
            <li>this is li6</li>
            <li>this is li7</li>
            <li>this is li8</li>
            <li>this is li9</li>
        </ul>
        <script>
            window.onload = function() {
                var oUl = document.getElementsByTagName("ul")[0];
                var oLi = document.getElementsByTagName("li")[0];
                oUl.appendChild(oLi);
            };
        </script>
    </body>
</html>
```

## Node.prototype.hasChildNodes()

`hasChildNodes` 方法返回一个布尔值，表示当前节点是否有子节点。

注意，子节点包括所有类型的节点，并不仅仅是元素节点。
哪怕节点只包含一个空格，`hasChildNodes` 方法也会返回 `true`。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">div1</div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log(oDiv.hasChildNodes());
        };
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
    </head>
    <body>
        <div id="div1"><!-- div1 --></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log(oDiv.hasChildNodes());
        };
    </script>
</html>
```

判断一个节点有没有子节点，有许多种方法，下面是其中的三种。

1. `node.hasChildNodes()`
2. `node.firstChild !== null`
3. `node.childNodes && node.childNodes.length > 0`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1"></div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log(oDiv.firstChild !== null);
        };
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
    </head>
    <body>
        <div id="div1">11111</div>
    </body>
    <script>
        window.onload = function() {
            oDiv = document.getElementById("div1");
            console.log(oDiv.childNodes && oDiv.childNodes.length > 0);
        };
    </script>
</html>
```

遍历全部节点

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">11111</div>
        <script>
            window.onload = function() {
                function showChild(parent, callback) {
                    callback(parent.nodeName + ":" + parent.nodeValue);
                    if (parent.hasChildNodes()) {
                        for (
                            var node = parent.firstChild;
                            node;
                            node = node.nextSibling
                        ) {
                            showChild(node, callback);
                        }
                    }
                }
                showChild(document.body, console.log);
            };
        </script>
    </body>
</html>
```

## Node.prototype.cloneNode()

`cloneNode` 方法用于克隆一个节点。
它接受一个布尔值作为参数，表示是否同时克隆子节点。
它的返回值是一个克隆出来的新节点。
在参数为 true 的情况下，执行深复制，也就是复制节点及其整个子节点树；在参数为 false 的情况下，执行浅复制， 即只复制节点本身。
复制后返回的节点副本属于文档所有，但并没有为它指定父节点。
因此，这个节点 副本就成为了一个“孤儿”，除非通过 `appendChild`() 、 `insertBefore`() 或 `replaceChild`() 将它添加到文档中

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <ul>
            <li>hello world0</li>
            <li>hello world1</li>
            <li>hello world2</li>
            <li>hello world3</li>
            <li>hello world4</li>
        </ul>
    </body>
    <script>
        window.onload = function() {
            var deepList = document
                .getElementsByTagName("ul")[0]
                .cloneNode(true);
            console.log(deepList.childNodes.length);
            var deepList = document
                .getElementsByTagName("ul")[0]
                .cloneNode(false);
            console.log(deepList.childNodes.length);
        };
    </script>
</html>
```

该方法有一些使用注意点。

1. 克隆一个节点，会拷贝该节点的所有属性，但是会丧失 `addEventListener` 方法和 `on`-属性（即 `node.onclick = fn`），添加在这个节点上的事件回调函数。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <input type="button" value="click me" />
    </body>
    <script>
        document.getElementsByTagName("input")[0].onclick = function() {
            console.log("hello world");
        };
        document.body.appendChild(
            document.getElementsByTagName("input")[0].cloneNode()
        );
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
    </head>
    <body>
        <input type="button" value="click me" />
    </body>
    <script>
        document.body.appendChild(
            document.getElementsByTagName("input")[0].cloneNode()
        );
        aInput = document.getElementsByTagName("input");
        for (var i = 0; i < aInput.length; i++) {
            aInput[i].onclick = function() {
                console.log("hello world");
            };
        }
    </script>
</html>
```

2. 该方法返回的节点不在文档之中，即没有任何父节点，必须使用诸如 `Node.appendChild` 这样的方法添加到文档之中。
3. 克隆一个节点之后，DOM 有可能出现两个有相同 id 属性（即 id="xxx"）的网页元素，这时应该修改其中一个元素的 id 属性。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #ccc;
                margin: 20px;
                float: left;
            }
        </style>
    </head>
    <body>
        <div id="div1"></div>
        <div id="div2"></div>
    </body>
    <script>
        oDiv1 = document.getElementById("div1");
        oDiv2 = document.getElementById("div2");
        var cloneDiv = document.getElementById("div1").cloneNode();
        // cloneDiv.getAttributeNode("id").nodeValue = "div3";
        cloneDiv.setAttribute("id", "div4");
        document.body.appendChild(cloneDiv);
        oDiv1.onclick = function() {
            alert("hello world");
        };
    </script>
</html>
```

## Node.prototype.insertBefore()

`insertBefore` 方法用于将某个节点插入父节点内部的指定位置。

`var insertedNode = parentNode.insertBefore(newNode, referenceNode);`

`insertBefore` 方法接受两个参数，
第一个参数是所要插入的节点 `newNode`，
第二个参数是父节点 `parentNode` 内部的一个子节点 `referenceNode`。
`newNode` 将插在 `referenceNode` 这个子节点的前面。返回值是插入的新节点 `newNode`

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <h1>hello world</h1>
    </body>
    <script>
        window.onload = function() {
            var p = document.createElement("p");
            p.innerHTML = "hello world";
            document.body.insertBefore(p, document.body.firstChild);
        };
    </script>
</html>
```

如果 `insertBefore` 方法的第二个参数为 null，则新节点将插在当前节点内部的最后位置，即变成最后一个子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <h1>hello world</h1>
    </body>
    <script>
        window.onload = function() {
            var p = document.createElement("p");
            p.innerHTML = "hello world";
            document.body.insertBefore(p);
        };
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
    </head>
    <body>
        <h1>hello world</h1>
    </body>
    <script>
        window.onload = function() {
            var p = document.createElement("p");
            p.innerHTML = "hello world";
            document.body.insertBefore(p, null);
        };
    </script>
</html>
```

注意，如果所要插入的节点是当前 DOM 现有的节点，则该节点将从原有的位置移除，插入新的位置。
就是, 择出来, 插回去, 个数不变

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <h1>hello world</h1>
        <h2>hello world</h2>
    </body>
    <script>
        window.onload = function() {
            var h2 = document.getElementsByTagName("h2")[0];
            document.body.insertBefore(h2, document.body.firstChild);
        };
    </script>
</html>
```

由于不存在 insertAfter 方法，如果新节点要插在父节点的某个子节点后面，可以用 insertBefore 方法结合 nextSibling 属性模拟。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <h1>hello world0</h1>
        <h2>hello world1</h2>
        <h3>hello world2</h3>
        <h4>hello world3</h4>
    </body>
    <script>
        window.onload = function() {
            var h1 = document.getElementsByTagName("h1")[0];
            document.body.insertBefore(
                h1,
                document.getElementsByTagName("h3")[0].nextSibling
            );
        };
    </script>
</html>
```

## Node.prototype.removeChild()

`removeChild` 方法接受一个子节点作为参数，用于从当前节点移除该子节点。返回值是移除的子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <h1>hello world0</h1>
        <h2>hello world1</h2>
        <h3>hello world2</h3>
        <h4>hello world3</h4>
    </body>
    <script>
        var oh4 = document.getElementsByTagName("h4")[0];
        oh4.parentNode.removeChild(oh4);
    </script>
</html>
```

如果参数节点不是当前节点的子节点，`removeChild` 方法将报错。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div>
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
        <div id="div1"></div>
    </body>
    <script>
        var oh4 = document.getElementsByTagName("h4")[0];
        var oDiv = document.getElementById("div1");
        oh4.parentNode.removeChild(oDiv);
    </script>
</html>
```

如何移除当前节点的所有子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="top">
            <h1>
                hello world0
                <span>!!!!!!!</span>
            </h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var element = document.getElementById("top");
        while (element.firstChild) {
            element.removeChild(element.firstChild);
        }
    </script>
</html>
```

被移除的节点依然存在于内存之中，但不再是 DOM 的一部分。所以，一个节点移除以后，依然可以使用它，比如插入到另一个节点下面。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="top">
            <h1>
                hello world0
                <span>!!!!!!!</span>
            </h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
        <div id="top2"></div>
    </body>
    <script>
        var element = document.getElementById("top");
        var element2 = document.getElementById("top2");
        while (element.firstChild) {
            var res = element.removeChild(element.firstChild);
            element2.appendChild(res);
        }
    </script>
</html>
```

## Node.prototype.replaceChild()

`replaceChild` 方法用于将一个新的节点，替换当前节点的某一个子节点。

`var replacedNode = parentNode.replaceChild(newChild, oldChild);`

上面代码中，`replaceChild` 方法接受两个参数，
第一个参数 `newChild` 是用来替换的新节点，
第二个参数 `oldChild` 是将要替换走的子节点。
返回值是替换走的那个节点 `oldChild`。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.getElementById("div1");
        var newSpan = document.createElement("span");
        newSpan.textContent = "Hello World!";
        div1.parentNode.replaceChild(newSpan, div1);
    </script>
</html>
```

## Node.prototype.contains()

`contains` 方法返回一个布尔值，表示参数节点是否满足以下三个条件之一。

1. 参数节点为当前节点。
2. 参数节点为当前节点的子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.getElementById("div1");
        var h2 = document.getElementsByTagName("h2")[0];
        console.log("↓↓↓↓↓↓ div1.contains(h2) ↓↓↓↓↓↓");
        console.log(div1.contains(h2));
    </script>
</html>
```

3. 参数节点为当前节点的后代节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.getElementById("div1");
        var h2 = document.getElementsByTagName("h2")[0];
        console.log("↓↓↓↓↓↓ document.body.contains(h2) ↓↓↓↓↓↓");
        console.log(document.body.contains(h2));
    </script>
</html>
```

注意，当前节点传入 contains 方法，返回 true。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.getElementById("div1");
        console.log("↓↓↓↓↓↓ div1.contains(div1) ↓↓↓↓↓↓");
        console.log(div1.contains(div1));
    </script>
</html>
```

## Node.prototype.isEqualNode()，Node.prototype.isSameNode()

`isEqualNode` 方法返回一个布尔值，用于检查两个节点是否相等。
所谓相等的节点，指的是两个节点的类型相同、属性相同、子节点相同。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.getElementById("div1");
        var div2 = document.getElementById("div1");
        console.log(div1.isEqualNode(div2));
        console.log(div1.isSameNode(div2));
    </script>
</html>
```

`isSameNode` 方法返回一个布尔值，表示两个节点是否为同一个节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div id="div1">
            <h1>hello world0</h1>
            <h2>hello world1</h2>
            <h3>hello world2</h3>
            <h4>hello world3</h4>
        </div>
    </body>
    <script>
        var div1 = document.createElement("div");
        var div2 = document.createElement("div");
        console.log(div1.isEqualNode(div2));
        console.log(div1.isSameNode(div2));
    </script>
</html>
```

## Node.prototype.normalize()

`normailize` 方法用于清理当前节点内部的所有文本节点（text）。
它会去除空的文本节点，并且将相邻的文本节点合并成一个，也就是说不存在空的文本节点，以及相邻的文本节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div></div>
        <script>
            window.onload = function() {
                var wrapper = document.createElement("div");

                wrapper.appendChild(document.createTextNode("Part 1 "));
                wrapper.appendChild(document.createTextNode("Part 2 "));

                // console.log(wrapper.childNodes.length);
                // console.log(wrapper.childNodes);
                // console.log(wrapper.firstChild);
                // console.log(wrapper.firstChild.nextSibling);
                wrapper.normalize();
                console.log(wrapper.childNodes.length);
                console.log(wrapper.childNodes);
                console.log(wrapper.firstChild);
            };
        </script>
    </body>
</html>
```

上面代码使用 normalize 方法之前，wrapper 节点有两个毗邻的文本子节点。使用 normalize 方法之后，两个文本子节点被合并成一个。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div></div>
        <script>
            window.onload = function() {
                var wrapper = document.createElement("div");

                wrapper.appendChild(document.createTextNode("Part 1 "));
                wrapper.appendChild(document.createElement("P"));
                wrapper.appendChild(document.createTextNode("Part 2 "));

                // console.log(wrapper.childNodes.length);
                // console.log(wrapper.childNodes);
                // console.log(wrapper.firstChild);
                // console.log(wrapper.firstChild.nextSibling);
                wrapper.normalize();
                console.log(wrapper.childNodes.length);//3
                console.log(wrapper.childNodes);//[text,p,text]
                console.log(wrapper.firstChild);//text
            };
        </script>
    </body>
</html>
```

## Node.prototype.getRootNode()

`getRootNode` 方法返回当前节点所在文档的根节点，与 `ownerDocument` 属性的作用相同。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div></div>
        <script>
            window.onload = function() {
                var res = document.body.firstChild.getRootNode() === document;
                console.log(res);

                var res1 =
                    document.body.firstChild.getRootNode() ===
                    document.body.firstChild.ownerDocument;
                console.log(res1);
            };
        </script>
    </body>
</html>
```

# 什么是 NodeList 和 HTMLCollection

节点都是单个对象，有时需要一种数据结构，能够容纳多个节点。DOM 提供两种节点集合，用于容纳多个节点：`NodeList` 和 `HTMLCollection`。
这两种集合都属于接口规范。许多 DOM 属性和方法，返回的结果是 NodeList 实例或 HTMLCollection 实例。
主要区别是，`NodeList` 可以包含各种类型的节点，`HTMLCollection` 只能包含 HTML 元素节点。

# NodeList 接口

## 概述

`NodeList` 实例是一个类似数组的对象，它的成员是节点对象。通过以下方法可以得到 `NodeList` 实例。

-   `Node.childNodes`
-   `document.querySelectorAll()`等节点搜索方法
    `document.body.childNodes instanceof NodeList // true`

    `document.querySelectorAll('body') instanceof NodeList`

    `NodeList` 实例很像数组，可以使用 `length` 属性和 `forEach` 方法。
    但是，它不是数组，不能使用 `pop` 或 `push` 之类数组特有的方法。
    `Array.isArray(document.body.childNodes)`

    `document.body.childNodes.length`

    `children.forEach(console.log)`
    上面代码中，NodeList 实例 children 不是数组，但是具有 length 属性和 forEach 方法。
    顺便提一下`foreach`

```javascript
var arr = ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"];
arr.forEach(console.log);
```

对象转数组
如果 NodeList 实例要使用数组方法，可以将其转为真正的数组。
`var children = document.body.childNodes;`

`var nodeArr = Array.prototype.slice.call(children);`

```javascript
var arr = ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"];
var obj = {
    0: "xujunhao",
    1: "good",
    2: "man",
    length: 3
};
// var res = [].slice.call(obj);
// console.log(res);
var arr = [];
for (var i = 0; i < obj.length; i++) {
    arr.push(obj[i]);
}
console.log(arr);
```

除了使用 `forEach` 方法遍历 `NodeList` 实例，还可以使用 `for` 循环。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var obj = document.body.childNodes;
                for (var i = 0; i < obj.length; i++) {
                    console.log(obj[i]);
                }
            };
        </script>
    </head>
    <body>
        <div><span></span></div>
    </body>
</html>
```

注意，NodeList 实例可能是动态集合，也可能是静态集合。
所谓动态集合就是一个活的集合，DOM 删除或新增一个相关节点，都会立刻反映在 NodeList 实例。
目前，只有 Node.childNodes 返回的是一个动态集合，其他的 NodeList 都是静态集合。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var children = document.body.childNodes;
                console.log(children.length);
                document.body.appendChild(document.createElement("p"));
                console.log(children.length);
            };
        </script>
    </head>
    <body>
        <div><span></span></div>
    </body>
</html>
```

`document.querySelectorAll()`就不行...

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var children = document.querySelectorAll("div");
                console.log(children.length);
                document.body.appendChild(document.createElement("div"));
                console.log(children.length);
            };
        </script>
    </head>
    <body>
        <div><span></span></div>
    </body>
</html>
```

## NodeList.prototype.length

`length` 属性返回 `NodeList` 实例包含的节点数量。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var objLength = document.querySelectorAll("span").length;
                console.log(objLength);
            };
        </script>
    </head>
    <body>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
    </body>
</html>
```

对于那些不存在的 HTML 标签，length 属性返回 0。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var objLength = document.querySelectorAll("p").length;
                console.log(objLength);
            };
        </script>
    </head>
    <body>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
        <div><span></span></div>
    </body>
</html>
```

支持自定义标签吗?

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var objLength = document.querySelectorAll("span").length;
                console.log(objLength);
            };
        </script>
    </head>
    <body>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

## NodeList.prototype.forEach()

`forEach` 方法用于遍历 `NodeList` 的所有成员。它接受一个回调函数作为参数，每一轮遍历就执行一次这个回调函数，用法与数组实例的 `forEach` 方法完全一致。

```javascript
var children = document.body.childNodes;
children.forEach(function f(item, i, list) {
    // ...
}, this);
```

上面代码中，回调函数 f 的三个参数依次是当前成员、位置和当前 NodeList 实例。forEach 方法的第二个参数，用于绑定回调函数内部的 this，该参数可省略。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                document.body.childNodes.forEach(function(a, b, c) {
                    console.log(b);
                }, this);
            };
        </script>
    </head>
    <body>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
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
        <script>
            window.onload = function() {
                document.body.childNodes.forEach(function(a, b, c) {
                    console.log(this.childNodes.item(b));
                }, document.getElementById("div1"));
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

## NodeList.prototype.item()

`item` 方法接受一个整数值作为参数，表示成员的位置，返回该位置上的成员。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.childNodes.item(1));
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

如果参数值大于实际长度，或者索引不合法（比如负数），item 方法返回 null。如果省略参数，item 方法会报错。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.childNodes.item(111));
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
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
        <script>
            window.onload = function() {
                console.log(document.body.childNodes.item());
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

所有类似数组的对象，都可以使用方括号运算符取出成员。一般情况下，都是使用方括号运算符，而不使用 item 方法。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.childNodes[1]);
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
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
        <script>
            window.onload = function() {
                console.log(document.body.childNodes[11111]);
            };
        </script>
    </head>
    <body>
        <div id="div1">
            <div><span111></span111></div>
        </div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

```javascript
var arr = ["The", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"];
console.log(arr[11111]);
```

## NodeList.prototype.keys()，NodeList.prototype.values()，NodeList.prototype.entries()

这三个方法都返回一个 ES6 的遍历器对象，可以通过 for...of 循环遍历获取每一个成员的信息。
区别在于，keys()返回键名的遍历器，values()返回键值的遍历器，entries()返回的遍历器同时包含键名和键值的信息。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var children = document.body.childNodes;
                for (var key of children.keys()) {
                    console.log(key);
                }
                for (var value of children.values()) {
                    console.log(value);
                }
                for (var entry of children.entries()) {
                    console.log(entry);
                }
            };
        </script>
    </head>
    <body>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
        <div><span111></span111></div>
    </body>
</html>
```

# HTMLCollection 接口

## 概述

`HTMLCollection` 是一个节点对象的集合，只能包含元素节点（`element`），不能包含其他类型的节点。
它的返回值是一个类似数组的对象，但是与 `NodeList` 接口不同，HTMLCollection 没有 `forEach` 方法，只能使用 `for` 循环遍历。
返回 `HTMLCollection` 实例的，主要是一些 `Document` 对象的集合属性，比如 `document.links、docuement.forms、document.images` 等。

### document.links

links 集合返回当期文档所有链接的数组。
提示： links 集合计算 <a href=""> 标签和 <area> 标签。

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
    </head>
    <body>
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1544033630190&di=f5c4771e31c4cb1951729a4bc86ba214&imgtype=0&src=http%3A%2F%2Fwww.yliywai.com%2Fyyact%2Fimages%2Fearth%2Ft1.jpg" usemap="#planetmap" />
        <map name="planetmap"><area shape="rect" coords="0,0,82,126" href="sun.htm" alt="Sun" /></map>
        <p><a href="http://www.baidu.com">百度一下</a></p>
        <p>
            链接/地址数目:
            <script>
                document.write(document.links.length);
            </script>
        </p>
    </body>
</html>
```

### docuement.forms

forms 集合可返回对文档中所有 Form 对象的引用。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <form name="Form1"></form>
        <form name="Form2"></form>
        <form name="Form3"></form>
        <script>
            document.write("This document contains: ");
            document.write(document.forms.length + " forms.");
        </script>
    </body>
</html>
```

### document.images

`images` 集合可返回对文档中所有 Image 对象的引用。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1544033630190&di=f5c4771e31c4cb1951729a4bc86ba214&imgtype=0&src=http%3A%2F%2Fwww.yliywai.com%2Fyyact%2Fimages%2Fearth%2Ft1.jpg" />
        <br />
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1544033630190&di=f5c4771e31c4cb1951729a4bc86ba214&imgtype=0&src=http%3A%2F%2Fwww.yliywai.com%2Fyyact%2Fimages%2Fearth%2Ft1.jpg" />
        <br />
        <br />
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1544033630190&di=f5c4771e31c4cb1951729a4bc86ba214&imgtype=0&src=http%3A%2F%2Fwww.yliywai.com%2Fyyact%2Fimages%2Fearth%2Ft1.jpg" />
        <br />
        <br />
        <img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1544033630190&di=f5c4771e31c4cb1951729a4bc86ba214&imgtype=0&src=http%3A%2F%2Fwww.yliywai.com%2Fyyact%2Fimages%2Fearth%2Ft1.jpg" />
        <br />
        <br />
        <script type="text/javascript">
            document.write("This document contains: ");
            document.write(document.images.length + " images.");
        </script>
    </body>
</html>
```

`document.links instanceof HTMLCollection`

`HTMLCollection` 实例都是动态集合，节点的变化会实时反映在集合中。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                var htmlForms = document.forms;
                var nodeForms = document.body.childNodes;
                console.log(htmlForms.length);
                console.log(nodeForms.length);
                document.body.appendChild(document.createElement("form"));
                console.log(htmlForms.length);
                console.log(nodeForms.length);
            };
        </script>
    </head>
    <body>
        <form name="Form1"></form>
        <form name="Form2"></form>
        <form name="Form3"></form>
    </body>
</html>
```

如果元素节点有 `id` 或 `name` 属性，那么 `HTMLCollection` 实例上面，可以使用 id 属性或 name 属性引用该节点元素。
如果没有对应的节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <img src="haha.jpg" alt="" id="img1" />
        <script>
            window.onload = function() {
                console.log(document.images.img1);
                console.log(document.images.img1.src);
            };
        </script>
    </body>
</html>
```

上面代码中，document.images 是一个 HTMLCollection 实例，可以通过<img>元素的 id 属性值，从 HTMLCollection 实例上取到这个元素。

## HTMLCollection.prototype.length

`length` 属性返回 `HTMLCollection` 实例包含的成员数量。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <a href="">0</a>
        <a href="">1</a>
        <a href="">2</a>
        <a href="">3</a>
        <a href="">4</a>
        <a href="">5</a>
        <a href="">6</a>
        <a href="">7</a>
        <a href="">8</a>
        <a href="">9</a>
        <a href="">10</a>
        <a href="">11</a>
        <a href="">12</a>
        <a href="">13</a>
        <a href="">14</a>
        <a href="">15</a>
        <a href="">16</a>
        <a href="">17</a>
        <a href="">18</a>
        <a href="">19</a>
        <a href="">20</a>
        <script>
            window.onload = function() {
                console.log(document.links.length);
            };
        </script>
    </body>
</html>
```

## HTMLCollection.prototype.item()

`item` 方法接受一个整数值作为参数，表示成员的位置，返回该位置上的成员。
由于方括号运算符也具有同样作用，而且使用更方便，所以一般情况下，总是使用方括号运算符。
如果参数值超出成员数量或者不合法（比如小于 0），那么 item 方法返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <a href="">this is tag a 0</a>
        <br />
        <a href="">this is tag a 1</a>
        <br />
        <a href="">this is tag a 2</a>
        <br />
        <a href="">this is tag a 3</a>
        <br />
        <a href="">this is tag a 4</a>
        <br />
        <a href="">this is tag a 5</a>
        <br />
        <a href="">this is tag a 6</a>
        <br />
        <a href="">this is tag a 7</a>
        <br />
        <a href="">this is tag a 8</a>
        <br />
        <a href="">this is tag a 9</a>
        <br />
        <a href="">this is tag a 10</a>
        <br />
        <a href="">this is tag a 11</a>
        <br />
        <a href="">this is tag a 12</a>
        <br />
        <a href="">this is tag a 13</a>
        <br />
        <a href="">this is tag a 14</a>
        <br />
        <a href="">this is tag a 15</a>
        <br />
        <a href="">this is tag a 16</a>
        <br />
        <a href="">this is tag a 17</a>
        <br />
        <a href="">this is tag a 18</a>
        <br />
        <a href="">this is tag a 19</a>
        <br />
        <a href="">this is tag a 20</a>
        <br />
        <script>
            window.onload = function() {
                console.log(document.links.item(3).innerHTML);
                console.log(document.links[4].innerHTML);
                console.log(document.links.item(33333));
                console.log(document.links.item(-33));
                console.log(document.links[33333]);
                console.log(document.links[-33]);
            };
        </script>
    </body>
</html>
```

## HTMLCollection.prototype.namedItem()

`namedItem` 方法的参数是一个字符串，表示 id 属性或 name 属性的值，返回对应的元素节点。
如果没有对应的节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <img id="pic" src="http://example.com/hello.jpg" name="hello" />
        <script>
            window.onload = function() {
                console.log(document.images.namedItem("pic"));
                console.log(document.images.namedItem("hello"));
            };
        </script>
    </body>
</html>
```

节点对象除了继承 `Node` 接口以外，还会继承其他接口。
`ParentNode`接口表示当前节点是一个父节点，提供一些处理子节点的方法。
`ChildNode`接口表示当前节点是一个子节点，提供一些相关方法。

# ParentNode 接口

如果当前节点是父节点，就会继承 ParentNode 接口。
由于只有元素节点（`element`）、文档节点（`document`）和文档片段节点（`documentFragment`）可以成为父节点，
因此只有这三类节点会继承`ParentNode`接口。

## ParentNode.children

`children`属性返回一个`HTMLCollection`实例，
成员是当前节点的所有元素子节点。该属性只读。
下面是遍历某个节点的所有元素子节点的示例。

```html
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
            window.onload = function() {
                for (var i = 0; i < document.childNodes.length; i++) {
                    console.log(document.childNodes[i]);
                }
            };
        </script>
    </body>
</html>
```

注意，`children`属性只包括元素子节点，不包括其他类型的子节点（比如文本子节点）。
如果没有元素类型的子节点，返回值 `HTMLCollection` 实例的 `length` 属性为 0。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.children.length);
            };
        </script>
    </head>
    <body>
        <div></div>
        hello world
    </body>
</html>
```

另外，`HTMLCollection` 是动态集合，会实时反映 DOM 的任何变化。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.children.length);
                document.body.appendChild(document.createElement("div"));
                console.log(document.body.children.length);
            };
        </script>
    </head>
    <body>
        <div></div>
        hello world
    </body>
</html>
```

## ParentNode.firstElementChild

`firstElementChild` 属性返回当前节点的第一个元素子节点。如果没有任何元素子节点，则返回 null。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.firstChild.nodeName);
                console.log(document.body.firstElementChild.nodeName);
            };
        </script>
    </head>
    <body>
        <div></div>
        hello world
    </body>
</html>
```

上面代码中，document 节点的第一个元素子节点是<HTML>。

## ParentNode.lastElementChild

`lastElementChild` 属性返回当前节点的最后一个元素子节点，如果不存在任何元素子节点，则返回 null。
`document.lastElementChild.nodeName`
上面代码中，document 节点的最后一个元素子节点是<HTML>（因为 document 只包含这一个元素子节点）。

## ParentNode.childElementCount

`childElementCount` 属性返回一个整数，表示当前节点的所有元素子节点的数目。如果不包含任何元素子节点，则返回 0。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <script>
            window.onload = function() {
                console.log(document.body.childElementCount);
            };
        </script>
    </head>
    <body>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        hello world
    </body>
</html>
```

## ParentNode.append()，ParentNode.prepend()

`append` 方法为当前节点追加一个或多个子节点，位置是最后一个元素子节点的后面。
该方法不仅可以添加元素子节点，还可以添加文本子节点。

```html
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
            window.onload = function() {
                var parent = document.body;
                // 添加元素子节点
                var p = document.createElement("p");
                parent.append(p);
                // 添加文本子节点
                parent.append("Hello");
                // 添加多个元素子节点
                var p1 = document.createElement("p");
                var p2 = document.createElement("p");
                parent.append(p1, p2);
                // 添加元素子节点和文本子节点
                var p = document.createElement("p");
                parent.append("Hello", p);
            };
        </script>
    </body>
</html>
```

注意，该方法没有返回值。
`prepend` 方法为当前节点追加一个或多个子节点，位置是第一个元素子节点的前面。
它的用法与 `append` 方法完全一致，也是没有返回值。

# ChildNode 接口

如果一个节点有父节点，那么该节点就继承了 `ChildNode` 接口。

## ChildNode.remove()

`remove` 方法用于从父节点移除当前节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div>this is div 0</div>
        <div>this is div 1</div>
        <div>this is div 2</div>
        <div>this is div 3</div>
        <div>this is div 4</div>
        <div>this is div 5</div>
        <div>this is div 6</div>
        <div>this is div 7</div>
        <div>this is div 8</div>
        <div>this is div 9</div>
    </body>
    <script>
        window.onload = function() {
            document.body.remove();
        };
    </script>
</html>
```

## ChildNode.before()，ChildNode.after()

`before` 方法用于在当前节点的前面，插入一个或多个同级节点。两者拥有相同的父节点。
如果是多个参数, 插入的是一个`整体`
注意，该方法不仅可以插入元素节点，还可以插入文本节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div>div1</div>
        <script>
            window.onload = function() {
                var p = document.createElement("p");
                var p1 = document.createElement("p");
                var oDiv = document.getElementsByTagName("div")[0];
                oDiv.before(p);
                oDiv.before("Hello");
                oDiv.before(p, p1);
                oDiv.before(p, "Hello");
            };
        </script>
    </body>
</html>
```

`after` 方法用于在当前节点的后面，插入一个或多个同级节点，两者拥有相同的父节点。用法与 `before` 方法完全相同。

## ChildNode.replaceWith()

`replaceWith` 方法使用参数节点，替换当前节点。参数可以是元素节点，也可以是文本节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div>div1</div>
        <script>
            window.onload = function() {
                var span = document.createElement("span");
                document.getElementsByTagName("div")[0].replaceWith(span);
            };
        </script>
    </body>
</html>
```

# Document 节点

## 概述

`document`节点对象代表整个文档，每张网页都有自己的`document`对象。`window.document`属性就指向这个对象。只要浏览器开始载入 HTML 文档，该对象就存在了，可以直接使用。

正常的网页，直接使用`document`或`window.document`。

## 属性

### 快捷方式属性

以下属性是指向文档内部的某个节点的快捷方式。

**1. document.doctype**

对于 HTML 文档来说，`document`对象一般有两个子节点。第一个子节点是`document.doctype`，指向`<DOCTYPE>`节点，即文档类型（Document Type Declaration，简写 DTD）节点。
HTML 的文档类型节点，一般写成`<!DOCTYPE html>`。如果网页没有声明 DTD，该属性返回`null`。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="x-ua-compatible" content="ie=edge" />
        <title>document</title>
    </head>
    <body>
        <script>
            window.onload = function() {
                console.log("↓↓↓↓↓↓ document.doctype ↓↓↓↓↓↓");
                console.log(document.doctype);
            };
        </script>
    </body>
</html>
```

`document.firstChild`通常就返回这个节点。

**2. document.documentElement**

`document.documentElement`属性返回当前文档的根元素节点（root）。
它通常是`document`节点的第二个子节点，紧跟在`document.doctype`节点后面。
HTML 网页的该属性，一般是`<html>`节点。

**3. document.body，document.head**

`document.body`属性指向`<body>`节点，`document.head`属性指向`<head>`节点。

这两个属性总是存在的，如果网页源码里面省略了`<head>`或`<body>`，浏览器会自动创建。
另外，这两个属性是可写的，如果改写它们的值，相当于移除所有子节点。
_如果是浏览器自动创建, 那么 script 的位置?_

**4. document.activeElement**

`document.activeElement`属性返回获得当前焦点（focus）的 DOM 元素。通常，这个属性返回的是`<input>`、`<textarea>`、`<select>`等表单元素，如果当前没有焦点元素，返回`<body>`元素或`null`。

### 节点集合属性

以下属性返回一个`HTMLCollection`实例，表示文档内部特定元素的集合。
这些集合都是动态的，原节点有任何变化，立刻会反映在集合中。

**1. document.links**

`document.links`属性返回当前文档所有设定了`href`属性的`<a>`及`<area>`节点。

**2. document.forms**

`document.forms`属性返回所有`<form>`表单节点。

除了使用位置序号，`id`属性和`name`属性也可以用来引用表单。

```javascript
/* HTML 代码如下
  <form name="foo" id="bar"></form>
*/
document.forms[0] === document.forms.foo; // true
document.forms.bar === document.forms.foo; // true
```

**3. document.images**

`document.images`属性返回页面所有`<img>`图片节点。

```javascript
var imglist = document.images;

for (var i = 0; i < imglist.length; i++) {
    if (imglist[i].src === "banner.gif") {
        // ...
    }
}
```

上面代码在所有`img`标签中，寻找某张图片。

**4. document.scripts**

`document.scripts`属性返回所有`<script>`节点。

```javascript
var scripts = document.scripts;
if (scripts.length !== 0) {
    console.log("当前网页有脚本");
}
```

### 文档静态信息属性

以下属性返回文档信息。

**（1）document.documentURI，document.URL**

`document.documentURI`属性和`document.URL`属性都返回一个字符串，表示当前文档的网址。
不同之处是它们继承自不同的接口，
`documentURI`继承自`Document`接口，可用于所有文档；
`URL`继承自`HTMLDocument`接口，只能用于 HTML 文档。

```javascript
document.URL;
// http://www.example.com/about

document.documentURI === document.URL;
// true
```

如果文档的锚点（`#anchor`）变化，这两个属性都会跟着变化。

**（2）document.domain**

`document.domain`属性返回当前文档的域名，不包含协议和接口。比如，网页的网址是`http://www.example.com:80/hello.html`，那么`domain`属性就等于`www.example.com`。

**（3）document.location**

`Location`对象是浏览器提供的原生对象，提供 URL 相关的信息和操作方法。通过`window.location`和`document.location`属性，可以拿到这个对象。

**（4）document.title**

`document.title`属性返回当前文档的标题。默认情况下，返回`<title>`节点的值。但是该属性是可写的，一旦被修改，就返回修改后的值。

```javascript
document.title = "新标题";
document.title; // "新标题"
```

## 方法

### document.open()，document.close()

`document.open`方法清除当前文档所有内容，使得文档处于可写状态，供`document.write`方法写入内容。

`document.close`方法用来关闭`document.open()`打开的文档。

```javascript
document.open();
document.write("hello world");
document.close();
```

### document.write()，document.writeln()

`document.write`方法用于向当前文档写入内容。

注意，`document.write`会当作 HTML 代码解析，不会转义。

```javascript
document.write("<p>hello world</p>");
```

上面代码中，`document.write`会将`<p>`当作 HTML 标签解释。

如果页面已经解析完成（`DOMContentLoaded`事件发生之后），再调用`write`方法，它会先调用`open`方法，擦除当前文档所有内容，然后再写入。

```javascript
document.addEventListener("DOMContentLoaded", function(event) {
    document.write("<p>Hello World!</p>");
});

// 等同于
document.addEventListener("DOMContentLoaded", function(event) {
    document.open();
    document.write("<p>Hello World!</p>");
    document.close();
});
```

如果在页面渲染过程中调用`write`方法，并不会自动调用`open`方法。（可以理解成，`open`方法已调用，但`close`方法还未调用。）

```html
<html>
    <body>
        hello
        <script type="text/javascript">
            document.write("world");
        </script>
    </body>
</html>
```

在浏览器打开上面网页，将会显示`hello world`。

`document.write`是 JavaScript 语言标准化之前就存在的方法，现在完全有更符合标准的方法向文档写入内容（比如对`innerHTML`属性赋值）。所以，除了某些特殊情况，应该尽量避免使用`document.write`这个方法。

`document.writeln`方法与`write`方法完全一致，除了会在输出内容的尾部添加换行符。

```javascript
document.write(1);
document.write(2);
// 12

document.writeln(1);
document.writeln(2);
// 1
// 2
//
```

注意，`writeln`方法添加的是 ASCII 码的换行符，渲染成 HTML 网页时不起作用，即在网页上显示不出换行。网页上的换行，必须显式写入`<br>`。

### document.querySelector()，document.querySelectorAll()

`document.querySelector`方法接受一个 CSS 选择器作为参数，返回匹配该选择器的元素节点。如果有多个节点满足匹配条件，则返回第一个匹配的节点。如果没有发现匹配的节点，则返回`null`。

```javascript
var el1 = document.querySelector(".myclass");
```

`document.querySelectorAll`方法与`querySelector`用法类似，区别是返回一个`NodeList`对象，包含所有匹配给定选择器的节点。

```javascript
elementList = document.querySelectorAll(".myclass");
```

这两个方法的参数，可以是逗号分隔的多个 CSS 选择器，返回匹配其中一个选择器的元素节点，这与 CSS 选择器的规则是一致的。

```javascript
var matches = document.querySelectorAll("div.note, div.alert");
```

上面代码返回`class`属性是`note`或`alert`的`div`元素。

这两个方法都支持复杂的 CSS 选择器。

```javascript
// 选中 name 属性等于 someval 的元素
document.querySelectorAll('[name="someval"]');

// 选中div元素，那些 class 含 ignore 的除外
document.querySelectorAll("DIV:not(.ignore)");

// 同时选中 div，a，script 三类元素
document.querySelectorAll("DIV, A, SCRIPT");
```

但是，它们不支持 CSS 伪元素的选择器（比如`:first-line`和`:first-letter`）和伪类的选择器（比如`:link`和`:visited`），即无法选中伪元素和伪类。

如果`querySelectorAll`方法的参数是字符串`*`，则会返回文档中的所有元素节点。另外，`querySelectorAll`的返回结果不是动态集合，不会实时反映元素节点的变化。

最后，这两个方法除了定义在`document`对象上，还定义在元素节点上，即在元素节点上也可以调用。

### document.getElementsByTagName()

`document.getElementsByTagName`方法搜索 HTML 标签名，返回符合条件的元素。它的返回值是一个类似数组对象（`HTMLCollection`实例），可以实时反映 HTML 文档的变化。如果没有任何匹配的元素，就返回一个空集。

```javascript
var res = document.getElementsByTagName("p");
res instanceof HTMLCollection; // true
```

上面代码返回当前文档的所有`p`元素节点。

HTML 标签名是大小写不敏感的，因此`getElementsByTagName`参数也是大小写不敏感的。另外，返回结果中，各个成员的顺序就是它们在文档中出现的顺序。

如果传入`*`，就可以返回文档中所有 HTML 元素。

```javascript
var allElements = document.getElementsByTagName("*");
```

注意，元素节点本身也定义了`getElementsByTagName`方法，返回该元素的后代元素中符合条件的元素。
也就是说，这个方法不仅可以在`document`对象上调用，也可以在任何元素节点上调用。

```javascript
var res = document.getElementsByTagName("p")[0];
var spans = res.getElementsByTagName("span");
```

上面代码选中第一个`p`元素内部的所有`span`元素。

### document.getElementsByClassName()

`document.getElementsByClassName`方法返回一个类似数组的对象（`HTMLCollection`实例），包括了所有`class`名字符合指定条件的元素，元素的变化实时反映在返回结果中。

```javascript
var elements = document.getElementsByClassName(names);
```

由于`class`是保留字，所以 JavaScript 一律使用`className`表示 CSS 的`class`。

参数可以是多个`class`，它们之间使用空格分隔。

```javascript
var elements = document.getElementsByClassName("foo bar");
```

上面代码返回同时具有`foo`和`bar`两个`class`的元素，`foo`和`bar`的顺序不重要。

注意，正常模式下，CSS 的`class`是大小写敏感的。（`quirks mode`下，大小写不敏感。）

与`getElementsByTagName`方法一样，`getElementsByClassName`方法不仅可以在`document`对象上调用，也可以在任何元素节点上调用。

```javascript
// 非document对象上调用
var elements = rootElement.getElementsByClassName(names);
```

### document.getElementsByName()

`document.getElementsByName`方法用于选择拥有`name`属性的 HTML 元素，返回一个类似数组的的对象（`NodeList`实例），因为`name`属性相同的元素可能不止一个。

```javascript
// 表单为 <form name="x"></form>
var forms = document.getElementsByName("x");
forms[0].tagName; // "FORM"
```

### document.getElementById()

`document.getElementById`方法返回匹配指定`id`属性的元素节点。
如果没有发现匹配的节点，则返回`null`。

```javascript
var elem = document.getElementById("para1");
```

注意，该方法的参数是大小写敏感的。比如，如果某个节点的`id`属性是`main`，那么`document.getElementById('Main')`将返回`null`。

`document.getElementById`方法与`document.querySelector`方法都能获取元素节点，不同之处是`document.querySelector`方法的参数使用 CSS 选择器语法，`document.getElementById`方法的参数是元素的`id`属性。

```javascript
document.getElementById("myElement");
document.querySelector("#myElement");
```

上面代码中，两个方法都能选中`id`为`myElement`的元素，但是`document.getElementById()`比`document.querySelector()`效率高得多。

另外，这个方法只能在`document`对象上使用，不能在其他元素节点上使用。

### document.createElement()

`document.createElement`方法用来生成元素节点，并返回该节点。

```javascript
var newDiv = document.createElement("div");
```

`createElement`方法的参数为元素的标签名，即元素节点的`tagName`属性，对于 HTML 网页大小写不敏感，即参数为`div`或`DIV`返回的是同一种节点。如果参数里面包含尖括号（即`<`和`>`）会报错。

```javascript
document.createElement("<div>");
// DOMException: The tag name provided ('<div>') is not a valid name
```

注意，`document.createElement`的参数可以是自定义的标签名。

```javascript
document.createElement("foo");
```

### document.createTextNode()

`document.createTextNode`方法用来生成文本节点（`Text`实例），并返回该节点。它的参数是文本节点的内容。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            #HELLO {
                width: 200px;
                height: 200px;
                background-color: #cccccc;
            }
        </style>
    </head>
    <body>
        <div id="hello" name="hello" class="hello1 hello">222</div>
    </body>
    <script>
        window.onload = function() {
            var newDiv = document.createElement("div");
            var newContent = document.createTextNode("Hello");
            newDiv.appendChild(newContent);
            document.body.appendChild(newDiv);
        };
    </script>
</html>
```

### document.createAttribute()

`document.createAttribute`方法生成一个新的属性节点（`Attr`实例），并返回它。

```javascript
var attribute = document.createAttribute(name);
```

`document.createAttribute`方法的参数`name`，是属性的名称。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div></div>
    </body>

    <script>
        window.onload = function() {
            var oDiv = document.getElementsByTagName("div")[0];
            var a = document.createAttribute("my_attr");
            a.value = "hello";
            oDiv.setAttributeNode(a);
            oDiv.setAttribute("my_attr2", "hello2");
        };
    </script>
</html>
```

上面代码为`div1`节点，插入一个值为`newVal`的`my_attr`属性。

### document.createComment()

`document.createComment`方法生成一个新的注释节点，并返回该节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div></div>
    </body>

    <script>
        window.onload = function() {
            var oDiv = document.getElementsByTagName("div")[0];
            var oComment = document.createComment("this is a comment");
            oDiv.appendChild(oComment);
        };
    </script>
</html>
```

`document.createComment`方法的参数是一个字符串，会成为注释节点的内容。

### document.addEventListener()，document.removeEventListener()

```javascript
// 添加事件监听函数
document.addEventListener("click", listener);

// 移除事件监听函数
document.removeEventListener("click", listener);
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #ccc;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>

    <script>
        window.onload = function() {
            var oDiv = document.getElementsByTagName("div")[0];
            function hello() {
                alert("hello world");
            }
            oDiv.addEventListener("click", hello);
        };
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
        <style>
            div {
                width: 200px;
                height: 200px;
                background-color: #ccc;
            }
        </style>
    </head>
    <body>
        <div></div>
    </body>

    <script>
        window.onload = function() {
            var oDiv = document.getElementsByTagName("div")[0];
            function hello() {
                alert("hello world");
            }
            oDiv.addEventListener("click", hello);
            oDiv.removeEventListener("click", hello);
        };
    </script>
</html>
```

### document.createNodeIterator()

`document.createNodeIterator`方法返回一个子节点遍历器。

```javascript
var nodeIterator = document.createNodeIterator(
    document.body,
    NodeFilter.SHOW_ELEMENT
);
```

上面代码返回`<body>`元素子节点的遍历器。

`document.createNodeIterator`方法第一个参数为所要遍历的根节点，第二个参数为所要遍历的节点类型，这里指定为元素节点（`NodeFilter.SHOW_ELEMENT`）。几种主要的节点类型写法如下。

-   所有节点：NodeFilter.SHOW_ALL
-   元素节点：NodeFilter.SHOW_ELEMENT
-   文本节点：NodeFilter.SHOW_TEXT
-   注释节点：NodeFilter.SHOW_COMMENT

`document.createNodeIterator`方法返回一个“遍历器”对象（`NodeFilter`实例）。该实例的`nextNode()`方法和`previousNode()`方法，可以用来遍历所有子节点。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <div>
            <span>span9</span>
            <div>
                <span>div_span_0</span>
                <span>div_span_1</span>
            </div>
        </div>
    </body>
    <script>
        window.onload = function() {
            var nodeIterator = document.createNodeIterator(
                document.body.firstElementChild
            );
            var arr = [];
            var currentNode;

            while ((currentNode = nodeIterator.nextNode())) {
                arr.push(currentNode);
            }
            console.log(arr);
        };
    </script>
</html>
```

# Element 节点

`Element`节点对象对应网页的 HTML 元素。每一个 HTML 元素，在 DOM 树上都会转化成一个`Element`节点对象（以下简称元素节点）。

元素节点的`nodeType`属性都是`1`。

```javascript
var p = document.querySelector("p");
p.nodeName; // "P"
p.nodeType; // 1
```
`Element`对象继承了`Node`接口，因此`Node`的属性和方法在`Element`对象都存在。

## 实例属性

### 元素特性的相关属性

**（1）Element.id**

`Element.id`属性返回指定元素的`id`属性，该属性可读写。

```javascript
// HTML 代码为 <p id="foo">
var p = document.querySelector("p");
p.id; // "foo"
```

注意，`id`属性的值是大小写敏感，即浏览器能正确识别`<p id="foo">`和`<p id="FOO">`这两个元素的`id`属性，但是最好不要这样命名。

**（2）Element.tagName**

`Element.tagName`属性返回指定元素的大写标签名，与`nodeName`属性的值相等。

```javascript
// HTML代码为
// <span id="myspan">Hello</span>
var span = document.getElementById("myspan");
span.id; // "myspan"
span.tagName; // "SPAN"
```

**（3）Element.lang**

`Element.lang`属性返回当前元素的语言设置。该属性可读写。

```javascript
// HTML 代码如下
// <html lang="en">
document.documentElement.lang; // "en"
```

### Element.attributes

`Element.attributes`属性返回一个类似数组的对象，成员是当前元素节点的所有属性节点

```javascript
var p = document.querySelector("p");
var attrs = p.attributes;

for (var i = attrs.length - 1; i >= 0; i--) {
    console.log(attrs[i].name + "->" + attrs[i].value);
}
```

上面代码遍历`p`元素的所有属性。

### Element.className，Element.classList

`className`属性用来读写当前元素节点的`class`属性。它的值是一个字符串，每个`class`之间用空格分割。

`classList`属性返回一个类似数组的对象，当前元素节点的每个`class`就是这个对象的一个成员。

```javascript
// HTML 代码 <div class="one two three" id="myDiv"></div>
var div = document.getElementById("myDiv");

div.className;
// "one two three"

div.classList;
// {
//   0: "one"
//   1: "two"
//   2: "three"
//   length: 3
// }
```

上面代码中，`className`属性返回一个空格分隔的字符串，而`classList`属性指向一个类似数组的对象，该对象的`length`属性（只读）返回当前元素的`class`数量。

`classList`对象有下列方法。

-   `add()`：增加一个 class。
-   `remove()`：移除一个 class。
-   `contains()`：检查当前元素是否包含某个 class。
-   `toggle()`：将某个 class 移入或移出当前元素。
-   `item()`：返回指定索引位置的 class。
-   `toString()`：将 class 的列表转为字符串。

```javascript
var div = document.getElementById("myDiv");

div.classList.add("myCssClass");
div.classList.add("foo", "bar");
div.classList.remove("myCssClass");
div.classList.toggle("myCssClass"); // 如果 myCssClass 不存在就加入，否则移除
div.classList.contains("myCssClass"); // 返回 true 或者 false
div.classList.item(0); // 返回第一个 Class
div.classList.toString();
```

下面比较一下，`className`和`classList`在添加和删除某个 class 时的写法。

```javascript
var foo = document.getElementById("foo");

// 添加class
foo.className += "bold";
foo.classList.add("bold");

// 删除class
foo.classList.remove("bold");
foo.className = foo.className.replace(/^bold$/, "");
```

`toggle`方法可以接受一个布尔值，作为第二个参数。如果为`true`，则添加该属性；如果为`false`，则去除该属性。

```javascript
el.classList.toggle("abc", boolValue);

// 等同于
if (boolValue) {
    el.classList.add("abc");
} else {
    el.classList.remove("abc");
}
```

### Element.innerHTML

`Element.innerHTML`属性返回一个字符串，等同于该元素包含的所有 HTML 代码。该属性可读写，常用来设置某个节点的内容。它能改写所有元素节点的内容，包括`<HTML>`和`<body>`元素。

如果将`innerHTML`属性设为空，等于删除所有它包含的所有节点。

```javascript
el.innerHTML = "";
```

上面代码等于将`el`节点变成了一个空节点，`el`原来包含的节点被全部删除。

注意，读取属性值的时候，如果文本节点包含`&`、小于号（`<`）和大于号（`>`），`innerHTML`属性会将它们转为实体形式`&amp;`、`&lt;`、`&gt;`。如果想得到原文，建议使用`element.textContent`属性。

```javascript
// HTML代码如下 <p id="para"> 5 > 3 </p>
document.getElementById("para").innerHTML;
// 5 &gt; 3
```

写入的时候，如果插入的文本包含 HTML 标签，会被解析成为节点对象插入 DOM。注意，如果文本之中含有`<script>`标签，虽然可以生成`script`节点，但是插入的代码不会执行。

```javascript
var name = "<script>alert('haha')</script>";
el.innerHTML = name;
```

上面代码将脚本插入内容，脚本并不会执行。但是，`innerHTML`还是有安全风险的。

```javascript
var name = "<img src=x onerror=alert(1)>";
el.innerHTML = name;
```

上面代码中，`alert`方法是会执行的。因此为了安全考虑，如果插入的是文本，最好用`textContent`属性代替`innerHTML`。

### Element.outerHTML

`Element.outerHTML`属性返回一个字符串，表示当前元素节点的所有 HTML 代码，包括该元素本身和所有子元素。

```javascript
// HTML 代码如下
// <div id="d"><p>Hello</p></div>
var d = document.getElementById("d");
d.outerHTML;
// '<div id="d"><p>Hello</p></div>'
```

`outerHTML`属性是可读写的，对它进行赋值，等于替换掉当前元素。

```javascript
// HTML 代码如下
// <div id="container"><div id="d">Hello</div></div>
var container = document.getElementById("container");
var d = document.getElementById("d");
container.firstChild.nodeName; // "DIV"
d.nodeName; // "DIV"

d.outerHTML = "<p>Hello</p>";
container.firstChild.nodeName; // "P"
d.nodeName; // "DIV"
```

上面代码中，变量`d`代表子节点，它的`outerHTML`属性重新赋值以后，内层的`div`元素就不存在了，被`p`元素替换了。但是，变量`d`依然指向原来的`div`元素，这表示被替换的`DIV`元素还存在于内存中。

注意，如果一个节点没有父节点，设置`outerHTML`属性会报错。

```javascript
var div = document.createElement("div");
div.outerHTML = "<p>test</p>";
// DOMException: This element has no parent node.
```

上面代码中，`div`元素没有父节点，设置`outerHTML`属性会报错。

### Element.children，Element.childElementCount

`Element.children`属性返回一个类似数组的对象（`HTMLCollection`实例），包括当前元素节点的所有子元素。如果当前元素没有子元素，则返回的对象包含零个成员。

```javascript
if (para.children.length) {
    var children = para.children;
    for (var i = 0; i < children.length; i++) {
        // ...
    }
}
```

上面代码遍历了`para`元素的所有子元素。

这个属性与`Node.childNodes`属性的区别是，它只包括元素类型的子节点，不包括其他类型的子节点。

`Element.childElementCount`属性返回当前元素节点包含的子元素节点的个数，与`Element.children.length`的值相同。

### Element.firstElementChild，Element.lastElementChild

`Element.firstElementChild`属性返回当前元素的第一个元素子节点，`Element.lastElementChild`返回最后一个元素子节点。

如果没有元素子节点，这两个属性返回`null`。

### Element.nextElementSibling，Element.previousElementSibling

`Element.nextElementSibling`属性返回当前元素节点的后一个同级元素节点，如果没有则返回`null`。

```javascript
// HTML 代码如下
// <div id="div-01">Here is div-01</div>
// <div id="div-02">Here is div-02</div>
var el = document.getElementById("div-01");
el.nextElementSibling;
// <div id="div-02">Here is div-02</div>
```

`Element.previousElementSibling`属性返回当前元素节点的前一个同级元素节点，如果没有则返回`null`。

## 实例方法

### 属性相关方法

元素节点提供六个方法，用来操作属性。

-   `getAttribute()`：读取某个属性的值
-   `getAttributeNames()`：返回当前元素的所有属性名
-   `setAttribute()`：写入属性值
-   `hasAttribute()`：某个属性是否存在
-   `hasAttributes()`：当前元素是否有属性
-   `removeAttribute()`：删除属性

### Element.querySelector()

`Element.querySelector`方法接受 CSS 选择器作为参数，返回父元素的第一个匹配的子元素。如果没有找到匹配的子元素，就返回`null`。

```javascript
var content = document.getElementById("content");
var el = content.querySelector("p");
```

上面代码返回`content`节点的第一个`p`元素。

`Element.querySelector`方法可以接受任何复杂的 CSS 选择器。

```javascript
document.body.querySelector("style[type='text/css'])");
```

注意，这个方法无法选中伪元素。

它可以接受多个选择器，它们之间使用逗号分隔。

```javascript
element.querySelector("div, p");
```

上面代码返回`element`的第一个`div`或`p`子元素。

需要注意的是，浏览器执行`querySelector`方法时，是先在全局范围内搜索给定的 CSS 选择器，然后过滤出哪些属于当前元素的子元素。因此，会有一些违反直觉的结果，下面是一段 HTML 代码。

```html
<div>
    <blockquote id="outer">
        <p>Hello</p>
        <div id="inner"><p>World</p></div>
    </blockquote>
</div>
```

那么，像下面这样查询的话，实际上返回的是第一个`p`元素，而不是第二个。

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <div>
        <blockquote id="outer">
            <p>Hello</p>
            <div id="inner"><p>World</p></div>
        </blockquote>
    </div>
    <script>
        window.onload = function() {
            var outer = document.getElementById("outer");
            console.log(outer.querySelector("div p"));
        };
    </script>
</html>
```

### Element.querySelectorAll()

`Element.querySelectorAll`方法接受 CSS 选择器作为参数，返回一个`NodeList`实例，包含所有匹配的子元素。

```javascript
var el = document.querySelector("#test");
var matches = el.querySelectorAll("div.highlighted > p");
```

该方法的执行机制与`querySelector`方法相同，也是先在全局范围内查找，再过滤出当前元素的子元素。因此，选择器实际上针对整个文档的。

它也可以接受多个 CSS 选择器，它们之间使用逗号分隔。如果选择器里面有伪元素的选择器，则总是返回一个空的`NodeList`实例。

### Element.getElementsByClassName()

`Element.getElementsByClassName`方法返回一个`HTMLCollection`实例，成员是当前元素节点的所有具有指定 class 的子元素节点。该方法与`document.getElementsByClassName`方法的用法类似，只是搜索范围不是整个文档，而是当前元素节点。

```javascript
element.getElementsByClassName("red test");
```

注意，该方法的参数大小写敏感。

由于`HTMLCollection`实例是一个活的集合，`document`对象的任何变化会立刻反应到实例，下面的代码不会生效。

```javascript
// HTML 代码如下
// <div id="example">
//   <p class="foo"></p>
//   <p class="foo"></p>
// </div>
var element = document.getElementById("example");
var matches = element.getElementsByClassName("foo");

for (var i = 0; i < matches.length; i++) {
    matches[i].classList.remove("foo");
    matches.item(i).classList.add("bar");
}
// 执行后，HTML 代码如下
// <div id="example">
//   <p></p>
//   <p class="foo bar"></p>
// </div>
```

上面代码中，`matches`集合的第一个成员，一旦被拿掉 class 里面的`foo`，就会立刻从`matches`里面消失，导致出现上面的结果。

### Element.getElementsByTagName()

`Element.getElementsByTagName`方法返回一个`HTMLCollection`实例，成员是当前节点的所有匹配指定标签名的子元素节点。该方法与`document.getElementsByClassName`方法的用法类似，只是搜索范围不是整个文档，而是当前元素节点。

```javascript
var table = document.getElementById("forecast-table");
var cells = table.getElementsByTagName("td");
```

注意，该方法的参数是大小写不敏感的。

### Element.matches()

`Element.matches`方法返回一个布尔值，表示当前元素是否匹配给定的 CSS 选择器。

```javascript
if (el.matches(".someClass")) {
    console.log("Match!");
}
```

### Element.remove()

`Element.remove`方法继承自 ChildNode 接口，用于将当前元素节点从它的父节点移除。

```javascript
var el = document.getElementById("mydiv");
el.remove();
```

上面代码将`el`节点从 DOM 树里面移除。

### Element.click()

`Element.click`方法用于在当前元素上模拟一次鼠标点击，相当于触发了`click`事件。

# 属性的操作

HTML 元素包括标签名和若干个键值对，这个键值对就称为“属性”（attribute）。

```html
<a id="test" href="http://www.example.com">链接</a>
```

上面代码中，`a`元素包括两个属性：`id`属性和`href`属性。

属性本身是一个对象（`Attr`对象），一般都是通过元素节点对象（`HTMlElement`对象）来操作属性。

## Element.attributes 属性

元素对象有一个`attributes`属性，返回一个类似数组的动态对象，成员是该元素标签的所有属性节点对象，属性的实时变化都会反映在这个节点对象上。其他类型的节点对象，虽然也有`attributes`属性，但返回的都是`null`，因此可以把这个属性视为元素对象独有的。

单个属性可以通过序号引用，也可以通过属性名引用。

```javascript
// HTML 代码如下
// <body bgcolor="yellow" onload="">
document.body.attributes[0];
document.body.attributes.bgcolor;
document.body.attributes["ONLOAD"];
```

注意，上面代码的三种方法，返回的都是属性节点对象，而不是属性值。

属性节点对象有`name`和`value`属性，对应该属性的属性名和属性值，等同于`nodeName`属性和`nodeValue`属性。

```javascript
// HTML代码为
// <div id="mydiv">
var n = document.getElementById("mydiv");

n.attributes[0].name; // "id"
n.attributes[0].nodeName; // "id"

n.attributes[0].value; // "mydiv"
n.attributes[0].nodeValue; // "mydiv"
```

## 属性操作的标准方法

### 概述

元素节点提供六个方法，用来操作属性。

-   `getAttribute()`
-   `getAttributeNames()`
-   `setAttribute()`
-   `hasAttribute()`
-   `hasAttributes()`
-   `removeAttribute()`

这有几点注意。

（1）适用性

这六个方法对所有属性（包括用户自定义的属性）都适用。

（2）返回值

`getAttribute()`只返回字符串，不会返回其他类型的值。

（3）属性名

这些方法只接受属性的标准名称，不用改写保留字，比如`for`和`class`都可以直接使用。另外，这些方法对于属性名是大小写不敏感的。

```javascript
var image = document.images[0];
image.setAttribute("class", "myImage");
```

上面代码中，`setAttribute`方法直接使用`class`作为属性名，不用写成`className`。

### Element.getAttribute()

`Element.getAttribute`方法返回当前元素节点的指定属性。如果指定属性不存在，则返回`null`。

```javascript
// HTML 代码为
// <div id="div1" align="left">
var div = document.getElementById("div1");
div.getAttribute("align"); // "left"
```

### Element.getAttributeNames()

`Element.getAttributeNames()`返回一个数组，成员是当前元素的所有属性的名字。如果当前元素没有任何属性，则返回一个空数组。使用`Element.attributes`属性，也可以拿到同样的结果，唯一的区别是它返回的是类似数组的对象。

```javascript
var mydiv = document.getElementById("mydiv");

mydiv.getAttributeNames().forEach(function(key) {
    var value = mydiv.getAttribute(key);
    console.log(key, value);
});
```

上面代码用于遍历某个节点的所有属性。

### Element.setAttribute()

`Element.setAttribute`方法用于为当前元素节点新增属性。如果同名属性已存在，则相当于编辑已存在的属性。该方法没有返回值。

```javascript
// HTML 代码为
// <button>Hello World</button>
var b = document.querySelector("button");
b.setAttribute("name", "myButton");
b.setAttribute("disabled", true);
```

上面代码中，`button`元素的`name`属性被设成`myButton`，`disabled`属性被设成`true`。

这里有两个地方需要注意，首先，属性值总是字符串，其他类型的值会自动转成字符串，比如布尔值`true`就会变成字符串`true`；其次，上例的`disable`属性是一个布尔属性，对于`<button>`元素来说，这个属性不需要属性值，只要设置了就总是会生效，因此`setAttribute`方法里面可以将`disabled`属性设成任意值。

### Element.hasAttribute()

`Element.hasAttribute`方法返回一个布尔值，表示当前元素节点是否包含指定属性。

```javascript
var d = document.getElementById("div1");

if (d.hasAttribute("align")) {
    d.setAttribute("align", "center");
}
```

上面代码检查`div`节点是否含有`align`属性。如果有，则设置为居中对齐。

### Element.hasAttributes()

`Element.hasAttributes`方法返回一个布尔值，表示当前元素是否有属性，如果没有任何属性，就返回`false`，否则返回`true`。

```javascript
var foo = document.getElementById("foo");
foo.hasAttributes(); // true
```

### Element.removeAttribute()

`Element.removeAttribute`方法移除指定属性。该方法没有返回值。

```javascript
// HTML 代码为
// <div id="div1" align="left" width="200px">
document.getElementById("div1").removeAttribute("align");
// 现在的HTML代码为
// <div id="div1" width="200px">
```

