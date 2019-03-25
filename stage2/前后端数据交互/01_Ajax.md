[TOC]

# ajax 简介

## 什么是 ajax?



AJAX = 异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。

> 当前页面发送一个请求给服务器，当前页面不需要等待服务器响应才能操作网页。发送完请求之后，当前页面可以继续浏览，操作。



简短地说，在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示

-   Ajax 主要的功能是实现了浏览器端 异步 访问服务器：
-   通过浏览器的 XMLHttpRequest 对象发出小部分数据，与服务端进行交互, 服务端返回小部分数据，然后更新客户端的部分页面。
-   json 是 Ajax 发送小部分数据的一种轻量级数据格式，可以简单易懂的给服务器或者浏览器交互数据


ajax的优点：

1. 最大的一点是页面无刷新，用户的体验非常好。
1. 使用异步方式与服务器通信，具有更加迅速的响应能力。
1. ajax的原则是“按需取数据”，可以最大程度的减少冗余请求，和响应对服务器造成的负担。
1. 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序。
1. ajax可使因特网应用程序更小、更快，更友好。

ajax的缺点：

1. ajax不支持浏览器back按钮。
1. 安全问题 AJAX暴露了与服务器交互的细节。
1. 对搜索引擎的支持比较弱。





![本文框架图](assets/163e8f98a78dc412)

#### 什么是Ajax

Ajax（Asynchronous JavaScript and XML的缩写）是一种异步请求数据的web开发技术，对于改善用户的体验和页面性能很有帮助。简单地说，在不需要重新刷新页面的情况下，Ajax 通过异步请求加载后台数据，并在网页上呈现出来。常见运用场景有表单验证是否登入成功、百度搜索下拉框提示和快递单号查询等等。
**Ajax目的：提高用户体验，较少网络数据的传输量**

#### Ajax原理是什么

在解释Ajax原理之前，我们不妨先举个“领导想找小李汇报一下工作”例子，

领导想找小李问点事，就委托秘书去叫小李，自己就接着做其他事情，直到秘书告诉他小李已经到了，最后小李跟领导汇报工作。
![领导想找小李汇报一下工作](assets/163e8f98a798685a)



Ajax请求数据流程与“领导想找小李汇报一下工作”类似。

其中最核心的依赖是浏览器提供的XMLHttpRequest对象，它扮演的角色相当于秘书，使得浏览器可以发出HTTP请求与接收HTTP响应。

浏览器接着做其他事情，等收到XHR返回来的数据再渲染页面。理解了Ajax的工作原理后，接下来我们探讨下如何使用Ajax。
![Ajax请求数据](assets/163e8f98a81cf781)




# jquery.ajax() 

jquery 库中已经封装了 ajax 请求的方法。
`jquery.ajax([settings])`。发请求并且能得知成功还是失败。

-   type:类型，"POST"或者"GET"，默认是"GET"。
-   url:发送请求的地址。
-   data：是一个对象，连同请求发送到服务器的数据
-   dataType：预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包含的 MIME 信息来智能判断，一般我们采用 json 格式，可以设置为"json"。
-   success:是一个方法，请求成功后的回调函数。传入返回后的数据，以及包含成功代码的字符串。
-   error:是一个方法、请求失败时调用此函数。传入 XMLHttpRequest 对象。
    

# jquery GET 请求

```javascript
$(document).ready(function() {
    $("#searchBtn").click(function() {
        $.ajax({
            type: "GET",
            url: " https://api.passport.xxx.com/checkNickname?username=" + mylogin.username + "&token=" + mylogin.token + "&nickname=" + nickname + "&format=jsonp&cb=?",
            dataType: "json",
            success: function(data) {
                if (data.errorCode == 0) {
                    $("#nickname").val(mylogin.nickname);
                } else {
                    $("#nickname").val("用户");
                }
            },
            error: function(jqXHR) {
                console.log("Error: " + jqXHR.status);
            }
        });
    });
});
```

# POST 请求

```javascript
function dologin(qrid, username, token) {
    $.ajax({
        url: "http://api.passport.pptv.com/v3/login/qrcode.do",
        type: "post",
        dataType: "jsonp",
        data: { from: "clt", qrid: qrid, username: username, token: token },
        success: function(data) {
            // do sth...
        }
    });
}
```

POST 请求，不需要去拼 url 字符串了，只需要指定 data，ajax 在传递的时候就会自动把它拼成 url。
Content-Type 是 ajax 为我们自动加上去的。
![img](assets/315302-20170224111728491-1605824346.png)
Form Data 在设置的时候，是用 JSON 对象的一个方式设置的。
![img](assets/315302-20170224111846945-1460720983.png)

![img](assets/315302-20170224112101320-1406587247.png)
但实际上在传递的时候，jquery 已经为我们拼成了 url 的格式，而且进行了一些转码。
![img](assets/315302-20170224112155382-1503467554.png)
POST 代码 demo：

```javascript
$.ajax({
    type:"POST",
    url:"service.php",
    dataType:"json",
    data{
        name:$("#staffName").val(),
        number:$("#staffNumber").val(),
        sex:$("#staffSex").val(),
        job:$("#staffJob").val(),
    },
    success:function(data){
        if(data.success){
            $("#createResult").html(data.msg);
        }else{
            $("#createResult").html("出现错误"+data.msg);
        }
    },
    error:function(jqXHR){
        console.log("发生错误："+jqXHR.status);
    }
});
```
