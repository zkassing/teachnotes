# ajax 简介 :

-   `Asynchronous JavaScript And XML` （异步的`JavaScript`和`XML`）
-   它并不是一种单一的技术，而是有机利用一系列交互式网页应用相关的技术所形成的结合体
-   `ajax` 是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换，`ajax` 可以使网页实现异步更新。
-   这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

## 优点：

1. 页面无刷新，用户体验好。
1. 异步通信，更加快的响应能力。
1. 减少冗余请求，减轻了服务器负担
1. 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序

## 缺点：

1. `ajax`干掉了`back`按钮，即对浏览器后退机制的破坏。
1. 存在一定的安全问题。
1. 对搜索引擎的支持比较弱。
1. 破坏了程序的异常机制。
1. 无法用`URL`直接访问

## `ajax`应用场景

-   场景 1. 数据验证
-   场景 2. 按需取数据
-   场景 3. 自动更新页面

## `ajax` 包含以下五个部分：

> `ajax`并非一种新的技术，而是几种原有技术的结合体。它由下列技术组合而成。

1. 使用`CSS`和`XHTML`来表示。
1. 使用`DOM`模型来交互和动态显示。
1. 数据互换和操作技术，使用`XML`与`XSLT`
1. 使用`XMLHttpRequest`来和服务器进行异步通信。
1. 使用`javascript`来绑定和调用。

> 在上面几中技术中，除了`XmlHttpRequest`对象以外，其它所有的技术都是基于`web`标准并且已经得到了广泛使用的，
> `XMLHttpRequest`虽然目前还没有被`W3C`所采纳，但是它已经是一个事实的标准，因为目前几乎所有的主流浏览器都支持它

## XHR 的属性和方法

![XMLHttpRequest对象的属性](assets/1480597-4c6beed36bb246c2.png)

![XMLHttpRequest对象的方法](assets/1480597-1092e842e08d9012.png)

# 使用 ajax

> `ajax`的原理简单来说通过`XmlHttpRequest`对象来向服务器发异步请求，
>
> 从服务器获得数据，然后用`javascript`来操作`DOM`而更新页面。
>
> 这其中最关键的一步就是从服务器获得请求数据。

## 使用原生 ajax 的 4 个步骤

-   创建`XMLHttpRequest`对象
-   准备请求
-   发送请求
-   处理响应

### 1. 创建`XMLHttpRequest`对象

-   `ajax`的核心是`XMLHttpRequest`对象，
-   它是`ajax`实现的关键，发送异步请求、接受响应以及执行回调都是通过它来完成
-   所有现代浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。

**创建 `XMLHttpRequest`对象的语法：**

```javascript
var xhr = new XMLHttpRequest();
```

**老版本的 `Internet Explorer`（IE5 和 IE6）使用`ActiveX` 对象：**

```javascript
var xhr = new ActiveXObject("Microsoft.XMLHTTP");
```

### 2. 准备请求

**初始化该`XMLHttpRequest`对象**

```javascript
xhr.open(method, url, async);
```

**参数说明**

1. 第一个参数表示请求类型的字符串，其值可以是`GET`或者`POST`
1. 第二个参数是要作为请求发送目标的 URL
1. 第三个参数是 `true` 或 `false` ，表示请求是以异步还是同步的模式发出。（默认为 `true` ，一般不建议为 `false` ）

```javascript
xhr.open("GET", "demo.php?name=tsrot&age=24", true);
```

### 3. 发送请求

```javascript
xhr.send();
```

#### `GET`请求:

-   一般情况下，使用`ajax`提交的参数多是些简单的字符串，
-   可以直接使用`GET`方法将要提交的参数写到`open`方法的`url`参数中，
-   此时`send`方法的参数为`null`或为空。

```javascript
xhr.open("GET", "demo.php?name=tsrot&age=24", true);
xhr.send(null);
```

#### `POST`请求：

-   如果需要像 `HTML` 表单那样 `POST` 数据，
-   请使用 `setRequestHeader()`来添加 `HTTP` 头。
-   然后在`send()`方法中规定您希望发送的数据：

```javascript
xhr.open("POST",'demo.php',true);
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded;charset=UTF-8");
xhr.send("id=123")`
```

### 4. 处理响应

```javascript
xhr.onreadystatechange = function() {
    // ajax成功
    if (xhr.readyState == 4 && xhr.status == 200) {
        console.log(xhr.responseText);
    }
};
```

#### `onreadystatechange`

-   当处理过程发生变化的时候执行下面的函数

#### `readyState` ：`ajax`处理过程

-   0：请求未初始化（还没有调用 `open()`）。
-   1：请求已经建立，但是还没有发送（还没有调用 `send()`）。
-   2：请求已发送，正在处理中（通常现在可以从响应中获取内容头）。
-   3：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。
-   4：响应已完成；您可以获取并使用服务器的响应了。

#### `status`属性：

-   200: OK
-   404: 未找到页面

#### `responseText`

-   获得字符串形式的响应数据

#### `responseXML`

-   获得 `XML`形式的响应数据

> 对象转换为 JSON 格式使用`JSON.stringify`
>
> `json`转换为对象格式用`JSON.parse()`
>
> 返回值一般为`json`字符串，可以用`JSON.parse(xhr.responseText)`转化为`JSON`对象

#### 原生 ajax 实现登录

```javascript
// 原生ajax
// 第一步: 创建对象
var xhr = new XMLHttpRequest();
// 第二步: 创建连接
xhr.open("post", "http://www.sina-show.com/api/user/login.php");
// 第三步: 发送请求
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded;charset=UTF-8");
xhr.send("userName=" + userName + "&" + "passWord=" + passWord);
// 第四步: 处理数据
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4) {
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304) {
            var res = JSON.parse(xhr.responseText); // 字符串转对象
            if (res.code) {
                // 如果接口拒绝...
                $(".notice").text(res.msg); // 展示拒绝信息
                $(".notice").addClass("warning"); // 拒绝信息加粗, 变红
                $("#logo_hov").addClass("heartBeat animated"); // 给登录界面加上动画
                // 1秒钟后, 关闭动画
                setTimeout(function() {
                    $("#logo_hov").removeClass("heartBeat animated");
                }, 1000);
            } else {
                // 登陆成功, 缓存user_id, 执行获取用户详情函数
                layer.msg("登录成功!", {
                    icon: 6
                });
                localStorage.setItem("user_id", res.data.id); // 缓存user_id
                get_user_info(); // 执行获取用户详情函数
            }
        } else {
            layer.msg("ajax请求失败!", {
                icon: 5
            });
        }
    }
};
```

#### 获取用户详情的一个例子(新浪项目)

```javascript
var userID = JSON.parse(localStorage.getItem("user"))["id"];
var xhr = new XMLHttpRequest();
xhr.open("post", "http://www.sina-ajax-js.com/api/user/info.php");
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded;charset=UTF-8");
xhr.send("id=1");
xhr.onreadystatechange = function() {
    if (xhr.readyState === 4) {
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
            var res = JSON.parse(xhr.responseText);
            if (res.code) {
                layer.msg(res.msg, {
                    icon: 5
                });
            } else {
                if (res.code) {
                    layer.msg(res.msg, {
                        icon: 5
                    });
                } else {
                    var tipContent = "";
                    var objComment = {
                        userName: "用户名",
                        name: "真实姓名",
                        NC: "昵称",
                        tel: "手机号",
                        email: "邮箱",
                        sex: "性别"
                    };
                    Object.keys(res.data).forEach(function(key) {
                        if (objComment[key]) {
                            if (key === "sex") {
                                res.data[key] = res.data[key] ? "男" : "女";
                            }
                            tipContent += objComment[key] + ": " + res.data[key] + "<br/>";
                        }
                    });
                    layer.tips(tipContent, "#getInfo");
                }
            }
        } else {
            layer.msg("ajax请求失败!", {
                icon: 5
            });
        }
    }
};
```

## 封装例子

### 将 `ajax` 请求封装成 `ajax()`方法，它接受一个配置对象 `params`

```javascript
function ajax(obj) {
    console.log("ajax is going...."); // 标记函数是否运行
    var xhr = new XMLHttpRequest(); // 新建一个对象
    xhr.open(obj.type, obj.url); // 建立连接
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded;charset=UTF-8"); // 解析post的字符串
    var sendStr = ""; // 声明一个新的字符串, 用来拼接, 对象转数组
    for (var i in obj.data) {
        sendStr += i + "=" + obj.data[i] + "&";
    }
    sendStr = sendStr.slice(0, -1); // 把最后的&符号删掉
    xhr.send(sendStr); // 发送请求
    xhr.onreadystatechange = function() {
        if (xhr.readyState === 4) {
            if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
                obj.success(xhr.responseText); // 如果成功, 调用对象的success方法
            } else {
                obj.error(xhr.responseText); // 如果失败, 调用对象的error方法
            }
        }
    };
}
```

### 使用实例(参照 `jquery` 的 `ajax`)：

```javascript
ajax({
    url: "test.php", // 请求地址
    type: "POST", // 请求类型，默认"GET"，还可以是"POST"
    data: { b: "异步请求" }, // 传输数据
    success: function(res) {
        // 请求成功的回调函数
        console.log(JSON.parse(res));
    },
    error: function(error) {} // 请求失败的回调函数
});
```

### 这个过程是一定要记在脑子里的

```javascript
function ajax(url, success, fail) {
    // 1. 创建对象
    var xhr = new XMLHttpRequest();
    // 2. 连接服务器
    xhr.open("get", url, true);
    // 3. 发送请求
    xhr.send(null);
    // 4. 接受请求
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4) {
            if (xhr.status == 200) {
                // 成功了, 做点事儿...
                success(xhr.responseText);
            } else {
                // 失败了, 做点事...
                fail && fail(xhr.status);
            }
        }
    };
}
```
