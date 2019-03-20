# CROS

>CORS是W3C标准, 全名叫跨域资源共享Cross-origin resource sharing<br>它允许浏览器向垮源服务器发出XMLHttpRequest请求. 
<br>CORS需要浏览器和服务器都支持

## 请求


+ 浏览器对于简单请求, 在请求报文中增加origin字段, 然后直接发送给服务器. origin字段表示请求来自哪个源(协议+域名+端口)
+ 服务器接收到请求后, 会发送一个HTTP响应, 若响应中包含Access-Control-Allow-Origin字段则表示发送请求的源在允许的范围内 
    + 若响应不包含Access-Control-Allow-Origin信息, 则表示出错了. 我们可以使用XMLHttpRequest.onerror的回调函数处理. 不能使用http状态码, 因为无论服务器是否允许源通信, 服务器都会发送响应给浏览器, 说明状态码为200
    + 服务器返回的响应除了Access-Control-Allow-Origin属性, 还会有其他属性如:
        + Access-Control-Allow-Origin :该字段是必须的。它的值要么是请求时origin字段的值，要么是一个*，表示接受任意域名的请求
        + Access-Control-Allow-Credentials: 可选字段, 为true表示允许发送Cookie. 同时, 发送时, 必须设置XMLHttpRequest.withCredentials为true才有效. 请求若服务器不允许浏览器发送, 删除该字段即可.
        + Access-Control-Expose-Headers: 可选字段, 指定发送请求时的其他头字段
# JSONP
>JSONP(JSON with Padding)是JSON的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。由于同源策略，一般来说位于 server1.example.com 的网页无法与不是 server1.example.com的服务器沟通，而 HTML 的script元素是一个例外。利用 script 元素的这个开放策略，网页可以得到从其他来源动态产生的 JSON 资料，而这种使用模式就是所谓的 JSONP。用 JSONP 抓到的资料并不是 JSON，而是任意的JavaScript，用 JavaScript 直译器执行而不是用 JSON 解析器解析。

## 使用
1. 在客户端调用提供JSONP支持的URL Service，获取JSONP格式数据。
比如客户想访问http://www.yiwuku.com/myService.aspx?jsonp=callbackFunction
假设客户期望返回JSON数据：["customername1","customername2"]
那么真正返回到客户端的Script Tags: callbackFunction([“customername1","customername2"])
可能的调用方式：
```
<script type="text/javascript" src="http://www.yiwuku.com/myService.aspx?jsonp=callbackFunction"></script>
```
2. 在客户端写callbackFunction函数的实现
```
<script type="text/javascript">
function CustomerLoaded(result,methodName)
{
    var html='<ul>';
    for(var i=0;i<result.length;i++)
    {
        html+='<li>'+result[i]+'</li>';
    }
    html+='</ul>';
    document.getElementById('divCustomers').innerHTML=html;
}
</script>
```
3. 页面展示
```
<div id="divCustomers"></div>
```

4. 最终Page Code
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Top Customers with Callback</title>
</head>
<body>
    <div id="divCustomers">
    </div>
    <script type="text/javascript">
        function onCustomerLoaded(result, methodName) {
            var html = '<ul>';
            for (var i = 0; i < result.length; i++) {
                html += '<li>' + result[i] + '</li>';
            }
            html += '</ul>';
            document.getElementById('divCustomers').innerHTML = html;
        }
    </script>
    <script type="text/javascript" src="http://www.yiwuku.com/myService.aspx?jsonp=onCustomerLoaded"></script>
</body>
</html>
```
### jquery中使用jsonp
1. $.getJSON
```
<script>
    $(document).ready(function(){
        $.getJSON("http://api.flickr.com/services/feeds/photos_public.gne?tags=cat&tagmode=any&format=json&jsoncallback=?",
        function(data){
        $.each(data.items,
        function(i,item){
        $("<img/>").attr("src",item.media.m).appendTo("#images");
        if(i==3)returnfalse;
        });
    });
});
```
>jsoncallback=?，其中 '？ '会自动替换为function(data)函数。
2. $.ajax
```
$.ajax({
    dataType:'jsonp',
    data:'id=10',
    jsonp:'jsonp_callback',
    url:'http://www.yiwuku.com/getdata',
    success:function(){
    //dostuff
    },
});
```
### 如何在服务器端实现对JSONP支持
>这仅仅需要把服务的JSON数据转换成想要的script tags的形式就可以了，格式可以自已定义，毕竟这是个非官方的协议。

#### php
```
echo "jsonp_callback(".json_encode(data).")";
```


# 与JSONP比较

> JSONP只支持GET请求, 以为动态创建的script标签只支持GET请求. 支持老式浏览器 <br>
>CORS支持所有的HTTP请求.

