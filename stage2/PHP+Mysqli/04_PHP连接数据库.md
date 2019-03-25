

# php 与 web 表单交互

在 PHP 中提供了两种与 Web 页面交互的方法，

一种是通过 Web 表单提交数据(`post`)，另一种是通过 URL 参数传递(`get`)。

## 表单

Web 表单的功能是让浏览者和网站有一个互动的平台。

Web 表单主要用来在网页中发送数据到服务器，

例如，提交注册信息时需要使用表单。

当用户填写完信息后做提交（submit）操作，即将表单的内容从客户端的浏览器传送到服务器端，经过服务器上的 PHP 程序进行处理后，再将用户所需要的信息传递回客户端的浏览器上。

通过获得用户信息，使 PHP 与 Web 表单实现了交互。

## 创建表单

> **使用<form>标记，并在其中插入相关的表单元素，即可创建一个表单。**

```html
<form name="form_name" method="method" action="url" enctype="value" target="target_win">… //省略插入的表单元素</form>
```

![1546946298758](assets/1546946298758.png)

![1546946325680](assets/1546946325680.png)

> GET()方法是将表单内容附加在 URL 地址后面发送；
> `http://www.baidu.com/index.php?username=xujunhao&userpwd=123456`
> POST()方法是将表单中的信息作为一个数据块发送到服务器上的处理程序中，在浏览器的地址栏不显示提交的信息。
> `http://www.baidu.com/index.php`
> method 属性默认方法为 GET()方法。

## 表单元素

> 表单（form）由表单元素组成。
>
> 常用的表单元素有以下几种标记：
>
> 输入域标记<input>、选择域标记<select>和<option>、文字域标记<textarea>等。

#### 输入域标记<input>

输入域标记<input>是表单中最常用的标记之一。

常用的输入域标记有文本框、按钮、单选按钮、复选框等。

语法格式如下：

```html
<form><input name="file_name" type="type_name" /></form>
```

参数 name 是指输入域的名称；参数 type 是指输入域的类型。

在<input…type="">标记中一共提供了 10 种类型的输入域，用户选择使用的类型由 type 属性决定。

type 属性取值及举例如表

![1546947142916](assets/1546947142916.png)

![img](assets/4a4572ff9449459ecb194b35ecdebfe9)



## 在普通的 Web 页中插入表单

```php
<!DOCTYPE html>
<html lang="zh">

<head>
    <script src="js/jquery.js"></script>
</head>

<body>
    <form action="" method="post">
        用户名:<input type="text" name="username"><br />
        用户密码:<input type="password" name="userpwd"><br />
        <input type="hidden" name="weight" value="260"><br/>
        <input type="submit" value="submit">
    </form>
</body>

</html>
<?php
// if ($_GET) {
//     var_dump($_GET);
// }
if ($_POST) {
    var_dump($_POST);
}
```



## 获取表单数据的两种方法

#### 使用 POST()方法提交表单

#### 使用 GET()方法提交表单



get和post的区别

-   GET 产生的 URL 地址可以被 Bookmark，而 POST 不可以。

*   GET 请求只能进行 url 编码，而 POST 支持多种编码方式。

-   GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留。

*   GET 请求在 URL 中传送的参数是有长度限制的，而 POST 么有。

-   对参数的数据类型，GET 只接受 ASCII 字符，而 POST 没有限制。

*   GET 比 POST 更不安全，因为参数直接暴露在 URL 上，所以不能用来传递敏感信息。

-   GET 参数通过 URL 传递，POST 放在 Request body 中。

# php书写简单计算器



#### 只写了加法的实例

```php
<?php
$msg = "";
$num1 = isset($_POST['num1']) ? $_POST['num1'] : "";
$num2 = isset($_POST['num2']) ? $_POST['num2'] : "";
$operator = isset($_POST['operator']) ? $_POST['operator'] : "";
if (isset($_POST)) {
    if ($num1 == "") {
        $msg .= "第一个数不能为空!<br/>";
    }
    if($num1 && !is_numeric($num1)){
        $msg .= "第一个数不是数字!<br/>";
    }
    if ($num2 == "") {
        $msg .= "第二个数不能为空!<br/>";
    }
    if($num2 && !is_numeric($num2)){
        $msg .= "第二个数不是数字!<br/>";
    }
    if (empty($msg)) {
        $sum = 0;
        switch ($operator) {
            case '+':
               $sum = $num1+$num2;
                break;
        }
    }
}
?>
<!DOCTYPE html>
<html lang="zh">
    <head>
        <title>简单计算器</title>
    </head>
    <body>
    <table align="center" border="1" width="500">
			<caption><h1>计算器</h1></caption>
			<form action="" method="post">
            
			<tr>
				<td>
					<input type="text" size="5" name="num1" value="<?php echo $num1 ?>" >
				</td>
				<td>
					<select name="operator">
						<option value="+" <?php if($operator == "+") echo "selected" ?>>+</option>
						<option value="-" <?php if($operator == "-") echo "selected" ?>>-</option>
						<option value="x" <?php if($operator == "x") echo "selected" ?>>x</option>
						<option value="/" <?php if($operator == "/") echo "selected" ?>>/</option>
						<option value="%" <?php if($operator == "%") echo "selected" ?>>%</option>
					</select>
				</td>
				<td>
					<input type="text" size="5" name="num2" value="<?php echo $num2 ?>">
				</td>
				<td>
					<input type="submit" name="sub" value="计算">
				</td>
            </tr>
            <?php 
            if ($_POST) {
                echo '<tr><td colspan="4" align="center" >';
                if (empty($msg)) {
                    echo "结果:{$num1} {$operator} {$num2} = {$sum}";
                }else{
                    echo $msg;
                }
                echo "</td></tr>";
            }
            ?>
    </form>
    </table>
    </body>
</html>

```



#### 完整代码

```php
<html>
	<head>
		<title>PHP实现简单计算器(使用分支结构)</title>
		<meta http-equiv="Content-Type" content="text/html;charset=utf-8">
	</head>
<?php
	$error="";    //声明一个错误消息变量，如果在表单中输入有误将错误消息放入该变量
	
	$num1 = isset($_POST["num1"]) ? $_POST["num1"] : "";                //初使化第一个数
	$num2 = isset($_POST["num2"]) ? $_POST["num2"] : "";                //初使化第二个数
	$operator = isset($_POST["operator"]) ? $_POST["operator"] : "";    //初使化运算符号

	//单路分支， 使用isset($_POST["sub"])判断用户是否有提交操作
	if(isset($_POST["sub"])) {   
		if($num1== "") {         //验证第一个数是否不空
			$error .= "第一个数不能为空<br>";

		}
		if(!is_numeric($num1)) { //验证第一个数是否为数字
			$error .= "第一个数不是数字<br>";
		}

		if($num2 == "") {        //验证第二个数是否不空
			$error .= "第二个数不能为空<br>";

		}
		if(!is_numeric($num2)) { //验证第二个数是否为数字
			$error .= "第二个数不是数字<br>";
		}
		

		if(empty($error)) {             //如果错误消息为空，说明输入正确的数据可以运算
			$sum = 0;          	//声明一个变量用来接收运算的结果
		
			switch($operator) {	//多路分支switch,判断用户使用的运算符号
				case "+":
					$sum = $num1 + $num2;   //加法运算
					break;
				case "-":
					$sum = $num1 - $num2;    //减法运算
					break;
				case "x":
					$sum = $num1 * $num2;    //乘法运算
					break;
				case "/":
					$sum = $num1 / $num2;    //除法运算
					break;
				case "%":
					$sum = $num1 % $num2;    //求模运算
					break;
			}
		}
	}
?>

	<body>
		<table align="center" border="1" width="500">
			<caption><h1>计算器</h1></caption>
			<form action="" method="post">
			<tr>
				<td>
					<?php  /*将用户输入的数据计算后还显示在输入表单中*/ ?>
					<input type="text" size="5" name="num1" value="<?php echo $num1 ?>" >
				</td>
				<td>
					<select name="operator">
						<?php /* 如果用户选择运算符后将其保留在界面上 */ ?>
						<option value="+" <?php if($operator == "+") echo "selected" ?>>+</option>
						<option value="-" <?php if($operator == "-") echo "selected" ?>>-</option>
						<option value="x" <?php if($operator == "x") echo "selected" ?>>x</option>
						<option value="/" <?php if($operator == "/") echo "selected" ?>>/</option>
						<option value="%" <?php if($operator == "%") echo "selected" ?>>%</option>
					</select>
				</td>
				<td>
					<input type="text" size="5" name="num2" value="<?php echo $num2 ?>">
				</td>
				<td>
					<input type="submit" name="sub" value="计算">
				</td>
			</tr>

			<?php
				//使用单路分支， 用户有提交操作才去执行结果
				if(isset($_POST["sub"])){
					echo '<tr><td colspan="5" align="center">';
					//双路分支，正解输入输出结果，有错误则输出错误消息
					if(empty($error)){
						echo "结果：{$num1} {$operator} {$num2} = {$sum}";
					}else{
						echo $error;
					}	
					echo '</td></tr>';
				}
			?>
			</form>
		</table>
	</body>
</html>

```



## php和javascript交互



```php
<?php
$a = "hello world";
?>


<script>

alert('<?php echo $a ?>');

</script>
```









## php和数据库交互

![1547003755523](assets/1547003755523.png)



#### msyqli

>  函数库, 函数名称都是以mysqli开始的



## 连接mysql服务器

![1547002026348](assets/1547002026348.png)

![1547002054727](assets/1547002054727.png)



```php
<?php
$host = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
if ($connID = mysqli_connect($host, $userName, $password)) {
    //建立与MySQL数据库的连接，并弹出提示对话框
    echo "<script type='text/javascript'>alert('数据库连接成功！');</script>";
} else {
    echo "<script type='text/javascript'>alert('数据库连接失败！');</script>";
}
?>

```





## 选择mysql数据库

#### 可以连接即选择

![1547002626054](assets/1547002626054.png)



#### 可以先连接再选择

![1547002791213](assets/1547002791213.png)



```php
<?php
$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password); //建立与MySQL数据库服务器的连接
if (mysqli_select_db($connID, $dbName)) { //选择数据库
    echo "数据库选择成功！";
} else {
    echo "数据库选择失败！";
}
?>
```





## 运行sql文件

![1547003103917](assets/1547003103917.png)



> link 必选 连接标识
>
> query 可选 sql语句

如果是select , 成功返回结果, 失败返回false

如果是增删改, 成功返回true, 失败返回false;



## 获取结果集



## 获取所有结果

`mysqli_fetch_all`

#### 结果返回数组

![1547006102634](assets/1547006102634.png)



> result mysqli_query返回的结果
>
> result_type 返回的表示方式
>
> > 1 : MYSQLI_ASSOC 关联数组
> >
> > 2 : MYSQLI_NUM 索引数组
> >
> > 3 : MYSQLI_BOTH 关联和索引数组



```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "select * from student");
// $arr = mysqli_fetch_row($result);
// while ($res = mysqli_fetch_array($result, 3)) {
//     var_dump($res);
//     echo "<br>";
// }

var_dump(mysqli_fetch_array($result,2));


while ($res = mysqli_fetch_array($result,2)) {
    var_dump($res);
}

```



#### 结果集中取一行(返回对象)

![1547006292827](assets/1547006292827.png)

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "select * from student");



while ($res = mysqli_fetch_object($result)) {
    var_dump($res);
}

```



#### 获取一行作为枚举数组



![1547006397095](assets/1547006397095.png)



```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "select * from student");



while ($res = mysqli_fetch_row($result)) {
    var_dump($res);
    echo $res[1];
    echo "\n";
}

```



#### 获取一行作为关联数组

![1547006454011](assets/1547006454011.png)

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "select * from student");



while ($res = mysqli_fetch_assoc($result)) {
    var_dump($res);
    echo $res['student_name'];
    echo "\n";
}

```



## 获取记录数

![1547006488157](assets/1547006488157.png)

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "select * from student");


var_dump(mysqli_num_rows($result)); // 19
```





## 增删改



## 增

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "INSERT INTO `student`(`student_name`, `student_sex`) VALUES ('张三999', 3)");

var_dump($result);
```



## 删

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接
// 严禁不加where进行删除或者更新操作
$result = mysqli_query($connID, "delete from student where student_id = 60");

var_dump($result);
```



## 改

```php
<?php

$host     = "127.0.0.1"; //MySQL服务器地址
$userName = "root"; //用户名
$password = "root"; //密码
$dbName   = "test"; //数据库名称
$connID   = mysqli_connect($host, $userName, $password, $dbName); //建立与MySQL数据库服务器的连接

$result = mysqli_query($connID, "UPDATE `test`.`student` SET `student_name` = '张三丰', `student_sex` = 1 WHERE `student_id` = 60");

var_dump($result);
```









