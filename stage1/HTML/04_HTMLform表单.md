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

### input 标签

**&lt;input&gt;** 标签根据不同的  **type** 属性，可以变化为多种形态。

####type类型：text

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

####type类型：radio
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

####type类型：checkbox

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
####type类型：password

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

####type类型：button

button 定义按钮

```
<input type="button" onclick="alert('Hello World!')" value="Click Me!">
```
<input type="button" onclick="alert('Hello World!')" value="Click Me!">

****

####type类型：submit

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

###<select> 元素（下拉列表）

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