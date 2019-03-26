# DOM事件
HTML DOM 允许 JavaScript 对 HTML 事件作出反应。
### 对事件作出反应

 当事件发生时，可以执行 JavaScript，比如当用户点击一个 HTML 元素时。

如需在用户点击某个元素时执行代码，请把 JavaScript 代码添加到 HTML 事件属性中：

```
onclick = javascript
```

HTML 事件的例子：

+ 当用户点击鼠标时
+ 当网页已加载时
+ 当图片已加载时
+ 当鼠标移动到元素上时
+ 当输入字段被改变时
+ 当 HTML 表单被提交时
+ 当用户触发按键时

**实例**

```
<!DOCTYPE html>
<html>
<body>
<h1 onclick="this.innerHTML='hello!'">请点击这段文本!</h1>
</body>
</html>
```
在上面的例子中，当用户点击时，会改变 \<h1> 元素的内容。

**实例**

```
<!DOCTYPE html>
<html>
<head>
<script>
function changetext(id)
{
id.innerHTML="hello!";
}
</script>
</head>
<body>
<h1 onclick="changetext(this)">请点击这段文本!</h1>
</body>
</html>
```
在上面的例子中，当用户点击时，会改变 \<h1> 元素的内容：会从事件处理程序中调用函数。

----

### HTML 事件属性

如需向 HTML 元素分配事件，我们可以使用事件属性。


**实例**

向 button 元素分配一个 onclick 事件：

```
<button onclick="displayDate()">试一试</button>
```
在上面的例子中，当点击按钮时，会执行名为 displayDate 的函数。

----

### 使用 HTML DOM 来分配事件

HTML DOM 允许您使用 JavaScript 向 HTML 元素分配事件：

为 button 元素分配 onclick 事件：

```
<script>
    document.getElementById("myBtn").onclick=function(){
        displayDate()
    };
</script>
```
在上面的例子中，名为 displayDate 的函数被分配给了 id=myButn" 的 HTML 元素。

当按钮被点击时，将执行函数。

----

|事件名|触发时机|
|:--|:--|
|onabort|图像的加载被中断。|
|onblur|元素失去焦点。|
|onchange|域的内容被改变。|
|onclick|当用户点击某个对象时调用的事件句柄。|
|ondblclick|当用户双击某个对象时调用的事件句柄。|
|onerror|在加载文档或图像时发生错误。|
|onfocus|元素获得焦点。|
|onkeydown|某个键盘按键被按下。|
|onkeypress|某个键盘按键被按下并松开。|
|onkeyup|某个键盘按键被松开。|
|onload|一张页面或一幅图像完成加载。|
|onmousedown|鼠标按钮被按下。|
|onmousemove|鼠标被移动。|
|onmouseout|鼠标从某元素移开。|
|onmouseover|鼠标移到某元素之上。|
|onmouseup|鼠标按键被松开。|
|onreset|重置按钮被点击。|
|onresize|窗口或框架被重新调整大小。|
|onselect|文本被选中。|
|onsubmit|确认按钮被点击。|
|onunload|用户退出页面。|

###  绑定事件监听函数

我们可以用 addEventListener() 或 attachEvent() 来绑定事件监听函数。

**addEventListener()函数语法：**

```
elementObject.addEventListener(eventName,handle,useCapture);
```
|参数|说明|
|:--|:--|
|elementObject|DOM对象（即DOM元素）。|
|eventName|事件名称。注意，这里的事件名称没有“ on ”，如鼠标单击事件 click ，鼠标双击事件 doubleclick ，鼠标移入事件 mouseover，鼠标移出事件 mouseout 等。|
|handle|事件句柄函数，即用来处理事件的函数。|
|useCapture|Boolean类型，是否使用捕获，一般用false |

**attachEvent()函数语法：**

```
elementObject.addEventListener(eventName,handle,useCapture);
```
|参数|说明|
|:--|:--|
|elementObject|DOM对象（即DOM元素）。|
|eventName|事件名称。注意，与addEventListener()不同，这里的事件名称有“ on ”，如鼠标单击事件 onclick ，鼠标双击事件 ondoubleclick ，鼠标移入事件 onmouseover，鼠标移出事件 onmouseout 等。|
|handle|事件句柄函数，即用来处理事件的函数。|

**注意：**addEventListener()是标准的绑定事件监听函数的方法，是W3C所支持的，Chrome、FireFox、Opera、Safari、IE9.0及其以上版本都支持该函数；但是，IE8.0及其以下版本不支持该方法，它使用attachEvent()来绑定事件监听函数。