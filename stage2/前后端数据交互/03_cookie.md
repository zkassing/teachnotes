[TOC]

# 什么是 cookie

![img](assets/15c34f0fb4614b5e646ec4e4ec5c2f62)

cookie 译为“小甜饼，具体种类称为酥性甜饼干，这是一种中档配料的产品……”。

-   当你在浏览网站的时候，WEB 服务器会先送一小小资料放在你的计算机上
-   cookie 会记录如身份识别号码、密码、用户在 Web 站点购物的方式或用户访问该站点的次数等关键信息
-   而正因为这些信息的重要性使 cookie 技术成为广大网民和开发人员争论的一个焦点
-   因为 cookie 将包含但不限于上述的一些信息保存在用户浏览器上的小文本文件上，它包含有关用户的信息。
-   这些相关信息保留下来可以为你下次再次访问该网站时鉴别用户，以便提供一些量身定做的内容。

![img](assets/0407ab414a367dd6155f5fe29bb481e4)

## 页面用来保存用户信息

-   可以往客户的机器上放一些东西(文本文件)

> 自动登录, 记住用户名

# cookie 的特性

-   同一个网站, 所有页面共享一套 cookie
-   数量, 大小限制
-   过期时间
-   存在客户端, 客户可以修改, 不安全, 不要存敏感信息

# cookie 原理

![img](assets/166579caafc9b0fb-1547592165484)

![img](assets/20662b52071692e2e6e8df7b8b241a01)

# cookie 长什么样子?

![1547592035195](assets/1547592035195.png)

# js 中使用 cookie

-   `document.cookie`

## 添加 cookie

### 一条 cookie

```javascript
document.cookie = "user_id=123";
```

### 多条 cookie

如果是不同的名字, 则会新增

如果是相同的名字(user_id), 则会覆盖

```javascript
document.cookie = "user_id=123";
document.cookie = "user_name=yunhe";
```

## 读取 cookie

```javascript
console.log(document.cookie);
```

# cookie 存在过期时间

> 如果没有设置, 重启浏览器, cookie 即消失...

## 为 cookie 指定过期时间

**设置一分钟以后过期**

```javascript
document.cookie = "user_id=123;Max-Age=" + 60;
```

> 推荐自己封装 cookie 的读写

# cookie 的属性

![img](assets/166579d6ac9d3008-1547592120608)

## Expires

> 具体到期时间，UTC 格式，默认为 null，若不设置，则浏览器关闭, 该 Cookie 就会被删除

```
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

## Max-Age 属性

> 指定从现在开始 Cookie 存在的秒数，比如 `60 * 60 * 24 * 365（即一年）`。
> 过了这个时间以后，浏览器就不再保留这个 Cookie。
> 如果同时指定了 Expires 和 Max-Age，那么 Max-Age 的值将优先生效。

## Domain

> Domain 设置域名，就是浏览器发出 Http 请求时，那些域名要带上这个 Cookie
> 若没有设置，则默认为当前 URL 的一级域名

www.example.com 会设为 example.com，而且以后如果访问 example.com 的任何子域名
HTTP 请求也会带上这个 Cookie
如果 Set-Cookie(服务器端) 字段指定的域名，不属于当前的域名，那么浏览器就会拒绝这个 Cookie

## Path

### cookie 的路径 Path

Path 属性可以为服务器特定文档指定 Cookie，这个属性设置的 url 且带有这个前缀的 url 路径都是有效的。

例如：`m.zhuanzhuan.58.com` 和 `m.zhaunzhuan.58.com/user/`这两个 url。
`m.zhuanzhuan.58.com` 设置 cookie

```
Set-cookie: id="123432";domain="m.zhuanzhuan.58.com";
```

`m.zhaunzhuan.58.com/user/` 设置 cookie：

```
Set-cookie：user="wang", domain="m.zhuanzhuan.58.com"; path=/user/
```

但是访问其他路径 `m.zhuanzhuan.58.com/other/`就会获得

```
cookie: id="123432"
```

如果访问 `m.zhuanzhuan.58.com/user/`就会获得

```
cookie: id="123432"  cookie: user="wang"
```

> Path 指定浏览器发出 http 请求之后，哪些路径要带上这个 Cookie
> 比如，PATH 属性是/，那么请求/docs 路径也会包含该 Cookie。当然，前提是域名必须一致。

## Secure

> Secure 属性指定浏览器只有在加密协议 HTTPS 下，才能将这个 Cookie 发送到服务器。
> 另一方面，如果当前协议是 HTTP，浏览器会自动忽略服务器发来的 Secure 属性。
> 该属性只是一个开关，不需要指定值。如果通信是 HTTPS 协议，该开关自动打开。

## HttpOnly

> HttpOnly 属性指定该 Cookie 无法通过 JavaScript 脚本拿到
> 主要是`Document.cookie`属性、`XMLHttpRequest`对象和 `Request API` 都拿不到该属性。
> 这样就防止了该 Cookie 被脚本读到，只有浏览器发出 HTTP 请求时，才会带上该 Cookie。

```javascript
document.cookie = "cookie1=value1; HttpOnly";
```

## domain

domain 限制了 cookie 的使用范围：只能在 domain 值的范围中才能访问到该 cookie.

同时 domain 值的设置也有严格的要求。

-   自身

    -   毫无疑问 domain 的值可以设置为本身。

-   向下：所有子域名

    -   如果我们当前页面的域名是 sub.test.com, 那么 domain 可以设置为.sub.test.com。允许所有 sub.test.com 的子域名访问，如 xx.sub.test.com、xx.xx.sub.test.com。

-   向上：父级域名,直到 Top-Level 的下一级
    -   如果我们当前页面的域名是 sub.test.com, 那么 domain 可以设置为 test.com。但是不能设置为.com。因为.com 属于[Top-Level Domain](https://link.juejin.im?target=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FTop-level_domain)。
    -   domain+path 共同限制了可访问该 cookie 的 URL。如果某个 cookie 的 path='/home'，那么只有“domain/home”下的所有 url 可以访问该 cookie。

> 最后，这些所有的属性值，一起决定了一件事——这个 cookie 那个 URL 可以能用。

# cookie 操作

## 封装操作

### 设置 cookie

```javascript
function setCookie(name, value, time) {
    if (time) {
        document.cookie = name + "=" + value + ";Max-Age=" + time;
    } else {
        document.cookie = name + "=" + value;
    }
}
```

### 获取 cookie

```javascript
function getCookie(name) {
    var arr = document.cookie.split("; ");
    for (var i = 0; i < arr.length; i++) {
        var arr2 = arr[i].split("=");
        if (arr2[0] === name) {
            return arr2[1];
        }
    }
    return "";
}
```

### 删除 cookie

```javascript
function removeCookie(name) {
    setCookie(name, "1", -1);
}
```

# 小练习

## 使用 cookie 保存拖拽位置

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>无标题文档</title>
        <style>
            #div1 {
                width: 200px;
                height: 200px;
                background: red;
                position: absolute;
            }
        </style>
        <script>
            window.onload = function() {
                var oDiv = document.getElementById("div1");
                var x = getCookie("x");
                var y = getCookie("y");
                if (x) {
                    oDiv.style.left = x + "px";
                    oDiv.style.top = y + "px";
                }

                oDiv.onmousedown = function(ev) {
                    var disX = ev.clientX - oDiv.offsetLeft;
                    var disY = ev.clientY - oDiv.offsetTop;
                    document.onmousemove = function(ev) {
                        oDiv.style.left = ev.clientX - disX + "px";
                        oDiv.style.top = ev.clientY - disY + "px";
                        setCookie("x", ev.clientX - disX);
                        setCookie("y", ev.clientY - disY);
                    };
                    document.onmouseup = function() {
                        document.onmousemove = null;
                        document.onmouseup = null;
                    };
                };
            };
            function setCookie(name, value, time) {
                if (time) {
                    document.cookie = name + "=" + value + ";Max-Age=" + time;
                } else {
                    document.cookie = name + "=" + value;
                }
            }
            function getCookie(name) {
                var arr = document.cookie.split("; ");
                for (var i = 0; i < arr.length; i++) {
                    var arr2 = arr[i].split("=");
                    if (arr2[0] === name) {
                        return arr2[1];
                    }
                }
                return "";
            }

            function removeCookie(name) {
                setCookie(name, "1", -1);
            }
        </script>
    </head>
    <body>
        <div id="div1"></div>
    </body>
</html>
```

## 保存表单的数据, 自动填充

```html
<!DOCTYPE html>
<html lang="zh">
    <head>
        <meta charset="UTF-8" />post
    </head>
    <body>
        <form action="">
            用户名:
            <input id="userName" type="text" />
            密码:
            <input id="passWord" type="password" />
            <input type="submit" value="登录" />
            <a href="javascript:;">忘记密码</a>
        </form>

        <script>
            window.onload = function() {
                oUserName = document.getElementById("userName");
                oPassWord = document.getElementById("passWord");
                if (getCookie("userName")) {
                    oUserName.value = getCookie("userName");
                }
                if (getCookie("passWord")) {
                    oPassWord.value = getCookie("passWord");
                }

                document.getElementsByTagName("form")[0].onsubmit = function() {
                    setCookie("userName", oUserName.value);
                    setCookie("passWord", oPassWord.value);
                };
                document.getElementsByTagName("a")[0].onclick = function() {
                    removeCookie("userName");
                    removeCookie("passWord");
                    oUserName.value = "";
                    oPassWord.value = "";
                };
            };
            function setCookie(name, value, time) {
                if (time) {
                    document.cookie = name + "=" + value + ";Max-Age=" + time;
                } else {
                    document.cookie = name + "=" + value;
                }
            }
            function getCookie(name) {
                var arr = document.cookie.split("; ");
                for (var i = 0; i < arr.length; i++) {
                    var arr2 = arr[i].split("=");
                    if (arr2[0] === name) {
                        return arr2[1];
                    }
                }
                return "";
            }

            function removeCookie(name) {
                setCookie(name, "1", -1);
            }
        </script>
    </body>
</html>
```

# `cookie`,`sessionStorage`, `localStorage`三者的异同：

## 生命周期：

-   cookie：可设置失效时间，没有设置的话，默认是关闭浏览器后失效
-   localStorage：除非被手动清除，否则将会永久保存。
-   sessionStorage： 仅在当前网页会话下有效，关闭页面或浏览器后就会被清除。

### 存放数据大小：

-   cookie：4KB 左右
-   localStorage 和 sessionStorage：可以保存 5MB 的信息。

### http 请求：

-   cookie：每次都会携带在 HTTP 头中，如果使用 cookie 保存过多数据会带来性能问题
-   localStorage 和 sessionStorage：仅在客户端（即浏览器）中保存，不参与和服务器的通信

### 易用性：

-   cookie：需要程序员自己封装，源生的 Cookie 接口不友好
-   localStorage 和 sessionStorage：源生接口可以接受，亦可再次封装来对 Object 和 Array 有更好的支持

## 应用场景：

-   从安全性来说，因为每次 http 请求都会携带 cookie 信息，这样无形中浪费了带宽，所以 cookie 应该尽可能少的使用，
-   另外 cookie 还需要指定作用域，不可以跨域调用，限制比较多。
-   但是用来识别用户登录来说，cookie 还是比 storage 更好用的。其他情况下，可以使用 storage，就用 storage。
-   storage 在存储数据的大小上面秒杀了 cookie，现在基本上很少使用 cookie 了，因为更大总是更好的
-   localStorage 和 sessionStorage 唯一的差别一个是永久保存在浏览器里面，一个是关闭网页就清除了信息。
-   localStorage 可以用来跨页面传递参数，sessionStorage 用来保存一些临时的数据，防止用户刷新页面之后丢失了一些参数。

## 浏览器支持情况：

localStorage 和 sessionStorage 是 html5 才应用的新特性，可能有些浏览器并不支持，这里要注意。

![img](assets/15ff2d54764e53af)

## 数据存放处：

![Cookie、localStorage、sessionStorage数据存放处](assets/15ff2f727028f37b)





Cookie、localStorage、sessionStorage 数据存放处

## 各浏览器 Cookie 大小、个数限制。

### 一、浏览器允许每个域名所包含的 cookie 数：

-   Microsoft 指出 InternetExplorer8 增加 cookie 限制为每个域名 50 个，但 IE7 似乎也允许每个域名 50 个 cookie。
-   Firefox 每个域名 cookie 限制为 50 个。
-   Opera 每个域名 cookie 限制为 30 个。
-   Safari/WebKit 貌似没有 cookie 限制。但是如果 cookie 很多，则会使 header 大小超过[服务器]()的处理的限制，会导致错误发生。

> “每个域名 cookie 限制为 20 个”将不再正确！

### 二、当很多的 cookie 被设置，浏览器如何去响应。

-   除 Safari（可以设置全部 cookie，不管数量多少），有两个方法：
-   最少最近使用（leastrecentlyused(LRU)）的方法：当 Cookie 已达到限额，自动踢除最老的 Cookie，以使给最新的 Cookie 一些空间。Internet Explorer 和 Opera 使用此方法。
-   Firefox 很独特：虽然最后的设置的 Cookie 始终保留，但似乎随机决定哪些 cookie 被保留。似乎没有任何计划（建议：在 Firefox 中不要超过 Cookie 限制）。

### 三、不同浏览器间 cookie 总大小也不同：

-   Firefox 和 Safari 允许 cookie 多达 4097 个字节，包括名（name）、值（value）和等号。
-   Opera 允许 cookie 多达 4096 个字节，包括：名（name）、值（value）和等号。
-   Internet Explorer 允许 cookie 多达 4095 个字节，包括：名（name）、值（value）和等号。

### 最后要说的

-   不要把什么数据都放在 Cookie、localStorage 和 sessionStorage 中，毕竟前端的安全性这么低。
-   只要打开控制台就可以任意的修改 Cookie、localStorage 和 sessionStorage 的数据了。
-   涉及到金钱或者其他比较重要的信息，还是要存在后台比较好。
