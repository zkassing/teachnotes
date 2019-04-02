# JavaScript 简介

## JavaScript 是什么

1. JavaScript 一种`解释型`、`弱类型`语言。
    1. 解释性语言, 编译型语言
        1. 解释性语言, 在线翻译, 英文文档
        2. 编译型语言, 英文书, 翻译成 30 国语言
    2. 弱类型语言, 强类型语言
2. 它的解释器被称为`JavaScript引擎`，为浏览器功能的一部分，广泛用于客户端的脚本语言。
3. 最早是在 HTML 网页上使用，用来给 HTML 网页`增加动态功能`的
4. 现在它被广泛用于开发网站特效、前后端交互、甚至后台开发（`Node.js`）。

### 什么是解释性语言, 什么是编译性语言?

-   高级语言： 人类可以看懂的语言（ 人类可以看懂， 电脑看不懂 ）
-   机器语言： 电脑可以看懂的语言（ 人类看不懂， 电脑可以看懂 ）
-   解释性语言的翻译时机： 读取一句， 解释一句， 运行一句
-   解释器（翻译角色）js 解释器也叫 js 引擎
-   编译性语言的翻译时机：先整体翻译， 转成机器码， 打包成操作系统可以识别的格式（exe）
-   编译器（翻译角色）

### 什么是弱类型语言, 什么是强类型语言?

-   弱类型语言：变量的数据类型改变， 不会报错， 没有问题（根据变量的值， 来确定变量类型）
-   强类型语言：变量的数据类型改变， 会报错（变量类型是提前声明的）
-   最主要的区别：数据类型是否可变

```javascript
// 有一个name是China；
var name = "China"; // 初始化语句， 声明一个变量name， 赋值“China”
name = "USA"; // 强类型， 弱类型都可以
name = 123; // 弱类型没问题， 强类型会报错
```

## JavaScript 发展史

-   JavaScript 最初诞生的原因，是网景公司（Netscape）为解决拨号上网时代（低带宽），服务端验证表单数据低效的问题，而着手开发一种客户端语言。
-   但在其发展过程中，早已不再局限于简单的表单数据验证，而是具备了与浏览器窗口及其内容等几乎所有方面的交互能力，并成为了一门全面的编程语言。
-   最初网景公司把这种客户端语言命名为 LiveScript，但为了搭上当时媒体热炒 Java 的顺风车，在发布前夕临时更名为 javascript。
-   随着微软等竞争对手推出 JScript 等 JavaScript 的不同实现，导致 JavaScript 的语法和特性日益混乱，其标准化问题被提上日程。
-   最终由欧洲计算机制造商协会（ECMA）以 JavaScript1.1 为蓝本，制定了【ECMA-262】标准，并由此标准定义了一种新脚本语言 ECMAScript。
-   随后，ISO 也采用 ECMAScript 作为标准，各浏览器厂商便纷纷开始将 ECMAScript 作为各自 JavaScript 实现的基础。

# JavaScript 的主要组成部分

## ECMAScript

> 作为核心，它规定了语言的组成部分：语法、类型、语句、关键字、保留字、操作符、对象

![](images/1.png)

### ECMAScript 是什么?

-   javascript 可以看成英语
-   ECMAScript 标准, 语法
-   为什么有标准, 就会存在兼容性问题?
-   不同浏览器, javascript 解释器不同, 对标准的执行严格程度(支持率)不同
-   解决兼容性, 只能增加代码量, 适配不同浏览器
-   越新的标准, 越不容易被兼容, 不要喜新厌旧, 稳定是第一位的.

## DOM

> DOM 把整个页面映射为一个多层节点结果，开发人员可借助 DOM 提供的 API，轻松地删除、添加、替换或修改任何节点。

![](images/2.png)

-   javascript 最主要做两件事
    1. 找对象
    2. 操作对象
-   兼容性问题(不同浏览器, DOM 支持的属性和方法不一样)
-   兼容性导致代码量上升

## BOM

> 支持可以访问和操作浏览器窗口的浏览器对象模型，开发人员可以控制浏览器显示的页面以外的部分。(兼容性很差)

### 兼容性问题

-   不用担心兼容性问题, 因为完全不兼容
-   不建议使用 BOM, 完全解决兼容性问题

# JavaScript 的特性

## 简单

JavaScript 语言中采用的是弱类型的变量类型,对使用的数据类型未做出严格的要求,是基于 Java 基本语句和控制的脚本语言,其设计简单紧凑。

## 动态

JavaScript 是一种采用事件驱动的脚本语言,它不需要经过 Web 服务器就可以对用户的输入做出响应。
在访问一个网页时,鼠标在网页中进行鼠标点击或上下移、窗口移动等操作 JavaScript 都可直接对这些事件给出相应的响应。

## 跨平台

JavaScript 脚本语言不依赖于操作系统,仅需要浏览器的支持。
因此一个 JavaScript 脚本在编写后可以带到任意机器上使用,前提上机器上的浏览器支持 JavaScript 脚本语言
目前 JavaScript 已被大多数的浏览器所支持。

> 不同于服务器端脚本语言，例如 PHP 与 ASP，JavaScript 主要被作为客户端脚本语言在用户的浏览器上运行，不需要服务器的支持。

> 所以在早期程序员比较青睐于 JavaScript 以减少对服务器的负担。

# JavaScript 的日常用途

-   嵌入动态文本于 HTML 页面。
-   对浏览器事件做出响应。
-   读写 HTML 元素。
-   在数据被提交到服务器之前验证数据。
-   检测访客的浏览器信息。
-   控制 cookies，包括创建和修改等。
-   基于 Node.js 技术进行服务器端编程。

# JavaScript 的优点和局限性

## 优点

1. 使用 JavaScript 可以在客户端进行数据验证，节省服务器端的资源。
2. 可以方便地操纵各种页面中的对象，使网页更加友好。
3. 使多种任务仅在客户端就可以完成而不需要网络和服务器的参与，从而支持分布式的运算和处理。

## 局限

1. 兼容性。互联网上有很多浏览器，如 FireFox，Internet Explorer、Opera 等，但各种浏览器支持 JavaScript 的程度是不一样的
2. JavaScript 不能打开、读写和保存用户计算机上的文件

# JavaScript 的引入方式

## 行内式

> 直接将脚本嵌入到 HTML 标记的事件中

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>js使用方式1：行内js</title>
    </head>
    <body>
        <input type="button" value="点击有惊喜" onclick="javascript:alert('哈哈哈哈')" />
        <!-- onclick:点击触发一个事件，alert：弹出一个对话框 -->
    </body>
</html>
```

## 嵌入式

> 使用`<script>`标记将脚本嵌入到网页中

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>js使用方式2：内部js</title>
        <script type="text/javascript">
            //声明一个函数(整个文档都可以使用)
            function surprise() {
                alert("恭喜你中了一百万"); /*弹出框*/
            }
        </script>
    </head>
    <body>
        <input type="button" value="点击有惊喜" onclick="surprise()" />
        <!--
            调用函数
        -->
        <input type="button" value="点击" onclick="surprise()" />
    </body>
</html>
```

## 链接式

> 通过`<script>`标记的`src`属性链接外部脚本文件

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <title>js使用方式3：外部js</title>
        <!-- 很多html页面都可以调用helloworld.js页面 -->
        <script src="./helloworld.js" type="text/javascript" charset="utf-8"></script>
    </head>
    <body>
        <input type="button" value="点击" onclick="hello()" />
    </body>
</html>
```

```javascript
function hello() {
    alert("hello world!!!");
}
```
