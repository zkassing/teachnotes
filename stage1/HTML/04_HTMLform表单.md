# HTML表单

> **HTML 表单用于搜集不同类型的用户输入。**

### <form>元素

> <form> 元素定义 HTML 表单：

**实例**

```
<form>
 .
form elements
 .
</form>
```

****

### HTML表单元素

表单元素指的是不同类型的 input 元素、文本域、复选框、单选按钮、提交按钮、下拉菜单等等。

****

### &lt;input&gt; 标签

**&lt;input&gt;** 标签根据不同的  **type** 属性，可以变化为多种形态。

#### type类型：text

text 定义常规文本输入。

```
<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

<form>
 First name:<br>
<input type="text" name="firstname">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

****

#### type类型：radio
radio 定义单选按钮输入（选择多个选择之一）
```
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

```
<form>
<input type="radio" name="sex" value="male" checked>Male
<br>
<input type="radio" name="sex" value="female">Female
</form> 

<br>
**注意：**如果想让单选框能够互斥，他们需要有相同的**name**属性，只有name值都为1的radio才可以同时只有一个被选中，如果name值不相同则可以同时被选中。

****

#### type类型：checkbox

复选框允许用户在有限数量的选项中选择零个或多个选项。

```
<form>
<input type="checkbox" name="vehicle" value="Bike">I have a bike
<br>
<input type="checkbox" name="vehicle" value="Car">I have a car 
</form> 
```
<form>
<input type="checkbox" name="vehicle" value="Bike">I have a bike
<br>
<input type="checkbox" name="vehicle" value="Car">I have a car 
</form> 

****
#### type类型：password

password定义密码框

```

<form>
 User name:<br>
<input type="text" name="username">
<br>
 User password:<br>
<input type="password" name="psw">
</form> 

```
****
<form>
 User name:<br>
<input type="text" name="username">
<br>
 User password:<br>
<input type="password" name="psw">
</form> 

<br>

**注意**：password 字段中的字符会被做掩码处理（显示为星号或实心圆）。

****

#### type类型：button

button 定义按钮

```
<input type="button" onclick="alert('Hello World!')" value="Click Me!">
```
<input type="button" onclick="alert('Hello World!')" value="Click Me!">

****

#### type类型：submit

定义提交表单数据至表单处理程序的按钮。

```

<form>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```

<form>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

****

### &lt;select&gt; 元素（下拉列表）

&lt;select&gt;标签定义下拉菜单

**实例**

```
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>

```

<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>


&lt;option&gt; 元素定义待选择的选项。
列表通常会把首个选项显示为被选选项。
可以通过 selected属性更改默认选中的项

```
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab" selected>Saab</option>
</select>

```

<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab" selected>Saab</option>
</select>

****


### &lt;textarea&gt; 标签

> &lt;textarea&gt; 元素定义多行输入字段（文本域）：

**实例**

```
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>

```
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>

****

### 用 &lt;fieldset&gt; 组合表单数据

&lt;fieldset&gt; 元素组合表单中的相关数据

&lt;legend&gt; 元素为 &lt;fieldset&gt; 元素定义标题。

**实例**

```
<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form> 

```

<form action="action_page.php">
<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit"></fieldset>
</form> 


****
### 表单元素的属性

|属性名|描述|
|:---|:------|
|name|如果要正确地被提交，每个输入字段必须设置一个 name 属性。|
|value|表单元素的初始值|
|readonly|规定表单元素的值为只读|
|disabled|属性规定输入字段是禁用的。|
|size|属性规定输入字段的尺寸（以字符计）：|
|maxlength|maxlength 属性规定输入字段允许的最大长度：|

### name 属性

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

**实例**

```
<form action="">
 First name:<br>
<input type="text" value="John">
<br>
 Last name:<br>
<input type="text" name="lastname">
<input type="submit">
</form> 

```

*这个例子只有lastname的值会被提交*

****

### value 属性

value 属性规定输入字段的初始值

**实例**

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```
*当你没有输入字符的时候输入框里显示的是value的值，当你输入值的时候value的值会被你输入的值覆盖*

****

### readonly 属性

readonly 属性规定输入字段为只读（不能修改）：


**实例**

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" readonly>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

*试试在First name 输入框里输入内容*

<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" readonly>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

**注意：readonly 属性不需要值。它等同于 readonly="readonly"。**

****

### disabled 属性

disabled 属性规定输入字段是禁用的。

被禁用的元素是不可用和不可点击的。

被禁用的元素不会被提交。

**实例**

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" disabled>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```
*尝试修改或者选取First name里的内容*

<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" disabled>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

****

### size 属性

size 属性规定输入框内容可见宽度（以字符计，与maxlength区别是size可以输入无限多的字符，而maxlength有长度限制）：

**实例**

```
<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" size="40">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```

<form action="">
 First name:<br>
<input type="text" name="firstname" value="John" size="20">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

****

### maxlength 属性

maxlength 属性规定输入字段允许的最大长度：

**实例**

```
<form action="">
 First name:<br>
<input type="text" name="firstname" maxlength="10">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```
*尝试在First name中输入超出长度限制的字符*

<form action="">
 First name:<br>
<input type="text" name="firstname" maxlength="10">
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

****

*********

# form标签的属性

|属性名|描述|
|:---|:------|
|action|规定向何处提交表单的地址（URL）（提交页面）。|
|method|规定在提交表单时所用的 HTTP 方法（默认：GET）。|
|name|规定识别表单的名称|
|autocomplete(H5新增)|属性规定表单或输入字段是否应该自动完成。当自动完成开启，浏览器会基于用户之前的输入值自动填写值。|
|novalidate(H5新增)|规定在提交表单时不对表单数据进行验证。（进本用不到）|

### action 属性

action 属性定义在提交表单时执行的动作。

向服务器提交表单的通常做法是使用提交按钮。

通常，表单会被提交到 web 服务器上的网页。

**实例**

```
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```
<form action="action_page.php">
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

在上面的例子中，指定了某个服务器脚本来处理被提交表单：

*如果省略 action 属性，则 action 会被设置为当前页面。*

****

### Method 属性

method 属性规定在提交表单时所用的 HTTP 方法（GET 或 POST，默认是get）：

```
<form action="action_page.php" method="GET">
```
或者
```
<form action="action_page.php" method="POST">
```

****

### Name 属性

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

本例只会提交 "Last name" 输入字段：

**实例**

```
<form action="action_page.php">
First name:<br>
<input type="text" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 

```

<form action="action_page.php">
First name:<br>
<input type="text" value="Mickey">
<br>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br><br>
<input type="submit" value="Submit">
</form> 