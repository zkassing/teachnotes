# 正式开始php

## 什么是php

> 服务器端的脚本语言
>
> PHP文件里可以写html代码









## php能干什么?

![1546783229761](images/1546783229761.png)



## 让PHP跑起来



开启apache, 把php解释器加入环境变量(非必须)





![1546782944716](images/1546782944716.png)



## php开始和结束标记`<?php ?>`

![1546784330501](images/1546784330501.png)

## php运行必须要加分号

![1546784348408](images/1546784348408.png)





## php 注释 `//`

![1546784308576](images/1546784308576.png)





apache默认路径

![1546832196858](images/1546832196858.png)

![1546831000151](images/1546831000151.png)



## 第一个程序 `hello world`

```php
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        hello world
    </body>
</html>
```
```php
<!DOCTYPE html>
<html lang="zh">
    <head>
        <script src="js/jquery.js"></script>
    </head>
    <body>
        <?php echo"hello world"; ?>
    </body>
</html>
```
```php
<?php
echo "hello world";

```

![1546784210222](images/1546784210222.png)





## 声明变量

php中, 变量使用`$`, 无论声明还是调用, 都需要

```php
<?php
$hello = "hello world";
echo $hello;

```

##  php不区分大小写?



变量区分大小写

关键字和函数不区分大小写

```php
<?php
$str = "hello world";
$STR = "HELLO WORLD";
echo $str."\n"; 
ECHO $STR."\n"; 
VAR_DUMP($str);

function hello(){
    echo "hello world";
}
HELLO();
```









## 变量命名规则

> 字母数字下划线, 不能以数字开头
>
> 不能使用关键字

![1546784781099](images/1546784781099.png)



## 可变变量

> 变量的名字, 可以动态的配置和使用

```php
<?php
$hi = "hello";
$$hi = "world";
echo $hello;
```



## 变量的引用赋值



> 一个消失, 另一个依然存在

```php
<?php
$a = "hello";
$b = $a;
echo $b;
$a = "world";
echo $b;

```



```php
<?php
$a = "hello";
$b = &$a;
echo $b;
$a = "world";
echo $b;

```

```php
<?php
$a = "hello";
$b = $a;
echo $b;
unset($a);
echo $b;

```



## 变量的作用域

![img](images/3da9b119efd9a873c07436d31780976d)

> 函数内的变量, 函数外不可用, 函数外的变量, 函数内不可以用
>
> 函数内要想使用函数外的变量, 需要加`global`

```php
<?php
$a = "hello";
function hello(){
    global $a; // 函数内要想使用函数外的变量, 需要加global
    echo $a;
}
hello();
```

函数外也可以使用函数内的变量

```php
<?php

function hello(){
    global $a;
    $a = 123;
}
hello();
echo $a;
```



静态变量在很多地方都能用到。

例如，在博客中使用静态变量记录浏览者的人数

```php
<?php
function show(){
    static $time = 0;
    echo "hello\n";
    $time++;
    echo $time."\n";
}
show();
show();
show();
show();
show();
show();
show();
```

#### php预定义变量

PHP还提供了很多非常实用的预定义变量，通过这些预定义变量可以获取到用户会话、用户操作系统的环境和本地操作系统的环境等信息。

![img](images/26afe2546380925fc5b2ac3d31834670)

![img](images/6de894c1d133a2b54a0f9880cd53dfd6)



# php变量的数据类型

![1546785763164](images/1546785763164.png)



## 使用`var_dump`函数, 可以查看数据类型

```php
<?php
var_dump("123");
var_dump(123);
var_dump(123.00);
var_dump(null);
var_dump(NULL);
var_dump([1,2,3]);


$arr = [
    "name"=>"yunhe",
    "sex"=>'female'
];

var_dump($arr);
class Person{
    
}
$obj = new Person; // new 一个对象
var_dump($obj);
```



#### 先说说标量



![img](images/9fbe2aad6a6dafa9fe1bf953666b43c3)



字符串类型

单双引号的区别

> 双引号中所包含的变量会自动被替换成实际数值，而单引号中包含的变量则按普通字符串输出。

```php
<?php

$a = "hello ";
echo $a."world";
```



```php
<?php

$a = "hello ";
echo "$a world";
```

```php
<?php

$a = "hello ";
echo "$aworld"; // 会把$aworld当成一个
```

```php
<?php

$a = "hello ";
echo "{$a}world";
```





在定义简单的字符串时，使用单引号是一个更加合适的处理方式。如果使用双引号，PHP将花费一些时间来处理字符串的转义和变量的解析。因此，在定义字符串时，**如果没有特别的要求，应尽量使用单引号**。



#### 浮点型

> 浮点型的数值只是一个近似值，所以要尽量避免浮点型数值之间比较大小，因为最后的结果往往是不准确的。



### 复合数据类型

![img](images/c8b2498f989c9c1c01d17c25636050f9)

#### 数组

数组是一组数据的集合，它把一系列数据组织起来，形成一个可操作的整体。

数组中可以包括很多数据，如标量数据、数组、对象、资源以及PHP中支持的其他语法结构等。

数组中的每个数据称为一个元素，元素包括索引（键名）和值两个部分。

元素的索引可以由数字或字符串组成，元素的值可以是多种数据类型。定义数组的语法格式如下

`php索引数组 == js的数组` `php关联数组 == js的对象`

`$array = ('value1',' value2 '……)`

```php
<?php

$a = [];
$a[0] = "hello";
var_dump($a);
```

```php
<?php

$a = array();
$a[0] = "hello";
var_dump($a);
```

```php
<?php

$a = array(1,2,3,4);
var_dump($a);
```

```php
<?php

$a = array('name'=>'yunhe');
var_dump($a);

```

```php
<?php

$a = [];

$a['name'] = "yunhe";

var_dump($a);

```



或

`$array[key] = 'value'`

或

`$array = array(key1 => value1, key2 => value2……)`

或

`$array = []`





## 对象

```php
<?php
class Person{
    var $name;
    function say(){
        echo "hello world";
    }
}

$p = new Person;
$p->name = "tom";
$p->say();
```



## 特殊数据类型

![img](images/187c160ef9bbe09e20fe4d1f21ef4535)





#### null

空值，顾名思义，表示没有为该变量设置任何值。

另外，空值（null）不区分大小写，null和NULL效果是一样的。

被赋予空值的情况有以下3种：还没有赋任何值、被赋值null、被unset()函数处理过的变量。

> is_null()函数用来判断变量是否为null，该函数返回一个boolean型，如果变量为null，则返回true，否则返回false。unset()函数用来销毁指定的变量。

unset

```php
<?php

$a = 123;
var_dump($a);
unset($a);
var_dump($a);
```

```php
<?php

$a = 123;
var_dump($a);
$a = null;
var_dump($a);

```

```php
<?php
$a;
var_dump($a);
var_dump(is_null($a));

```



## 数据类型转换

![img](images/7e24ab75a8d9af5022671e03a6eaed96)

```php
<?php
$a = 123;
var_dump($a);

var_dump((string)$a);
var_dump((float)$a);
var_dump((array)$a);
var_dump((object)$a);
```







在进行类型转换的过程中应该注意以下内容：

转换成boolean型时，null、0和未赋值的变量或空数组会被转换为false，其他的为true；

```php
<?php
$a;
var_dump((boolean)$a); // false
var_dump((boolean)[]); // false
var_dump((boolean)null); // false
var_dump((boolean)0); // false
var_dump((boolean)''); // false
var_dump((boolean)'0'); // false
var_dump((boolean)0.0); // false
var_dump((boolean)'0.0'); // true
```





转换成整型时，布尔型的false转换为0，true转换为1，浮点型的小数部分被舍去，字符型如果以数字开头就截取到非数字位，否则输出0。

```php
<?php
$a = "123hello";
var_dump((int)$a); // 123
$a = "hello123";
var_dump((int)$a); // 0

```





类型转换还可以通过`settype()`函数来完成，该函数可以将指定的变量转换成指定的数据类型。

`bool settype(mixed var, string type)`

参数var为指定的变量；

参数type为指定的数据类型。

参数type有7个可选值，即boolean、float、integer、array、null、object和string。

如果转换成功则`settype()`函数返回true，否则返回false

```php
<?php
$a = "123hello";
$b = settype($a,'integer');
var_dump($b); // boolean true
var_dump($a); // int 123

```







当字符串转换为整型或浮点型时，如果字符串是以数字开头的，就会先把数字部分转换为整型，再舍去后面的字符串；

如果数字中含有小数点，则会取到小数点前一位(int)。

```php
<?php
$a = "123.11hello";
$b = settype($a,'float');
var_dump($b); // boolean true
var_dump($a); // float 123.11
```



## 检测数据类型



PHP还内置了检测数据类型的系列函数，可以对不同类型的数据进行检测，判断其是否属于某个类型，如果符合则返回true，否则返回false。



> is_numeric 不仅可以判断整数和浮点数, 也可以判断全是数字的字符串

![img](images/21225f606bf02c233679150248f63b4a)

```php
<?php
$a = "123.11hello";
var_dump(is_string($a)); // true
$b = 123;
var_dump(is_numeric($b)); // true
var_dump(is_integer($b)); // true
var_dump(is_int($b)); // true

$c = 123.11;
var_dump(is_numeric($c)); // true
var_dump(is_float($c)); // true

$d = [];
var_dump(is_array($d)); // true

$e = "555";
var_dump(is_int($e));
var_dump(is_numeric($e)); // true 




```





## php常量



常量可以理解为值不变的量。

常量值被定义后，在脚本的其他任何地方都不能改变。

一个常量由英文字母、下划线和数字组成，但数字不能作为首字母出现。

在PHP中使用define()函数来定义常量，该函数的语法格式为：

`define(string constant_name,mixed value,case_sensitive=true)`



![img](images/6ce05345d1c7a6f2a1b0681d980c14df)



获取常量的值有两种方法：

一种是使用常量名直接获取值；

另一种是使用constant()函数，

constant()函数和直接使用常量名输出的效果是一样的，但函数可以动态地输出不同的常量，在使用上要灵活方便得多。

函数的语法格式为：

`mixed constant(string const_name)`

```php
<?php
define('HELLO', "hello world", true);

constant("HELLO");

```



要判断一个常量是否已经定义，可以使用defined()函数。

函数的语法格式为：

`bool defined(string constant_name);`



```php
<?php
define('HELLO', "hello world", true);

var_dump(defined('HELLO'));
```



参数`constant_name`为要获取常量的名称，成功则返回true，否则返回false。



## 预定义常量



![img](images/ea988dbfe9e8d161b6bc8f71e1c5a6f0)

> __FILE__和__LINE__中的“__”是两条下划线，而不是一条“_”。





# PHP运算符

## 算数运算符

![img](images/7ba35be4c0c9ed838d25831b17f03eb3)

## 字符串运算符

字符串运算符只有一个，即英文的句号“.”。它的作用是将两个字符串连接起来，结合成一个新的字符串。

注意，PHP中的“+”号只用作算术运算符使用，而不能用作字符串运算符



## 赋值运算符

![img](images/e04707960b68303b4de2202aa25919c3)

## 位运算符

![img](images/2438210a7b6d6316bd9458af514b1dd8)

## 逻辑运算符

![img](images/b328f87411d08ee5fd4f3b6a34baf9d9)

## 比较运算符

![img](images/531fbcdc9d0fa1492e02d2c8e25a6078)

>  xor 一样==> false 不一样==>true

## 错误控制运算符



错误控制运算符可以对程序中出现错误的表达式进行操作，进而对错误信息进行屏蔽，其使用的方法就是在错误的表达式前加上@即可。

@只是对错误信息进行屏蔽，并没有真正解决错误。

经常在程序中使用的某些函数出现一些不必要（不影响程序运行）的错误信息时，使用该运算符进行屏蔽。

而对程序中的一些影响程序运行的错误，使用它不是解决问题的根本办法，不推荐使用。

```php
<?php
$err = 5/0;
```



```php
<?php
@$err = 5/0;
```



## 三元运算符

三元运算符（?:），也称为三目运算符，其作用是根据一个表达式在另两个表达式中选择一个，而不是用来在两个语句或者程序中选择。三元运算符最好放在括号中使用



```php
<?php
$value = 100; //声明一个整型变量
echo ($value == true) ? '三元运算' : '没有该值'; //对整型变量进行判断

```



## 运算符的优先顺序和结合规则

> 优先级高的操作先执行，优先级低的操作后执行，同一优先级的操作按照从左到右的顺序进行。





| 结合方向 | 运算符                                                       | 附加信息                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 无       | clone new                                                    | [clone](http://php.net/manual/zh/language.oop5.cloning.php) 和 [new](http://php.net/manual/zh/language.oop5.basic.php#language.oop5.basic.new) |
| 左       | *[*                                                          | [array()](http://php.net/manual/zh/function.array.php)       |
| 右       | **\**                                                        | [算术运算符](http://php.net/manual/zh/language.operators.arithmetic.php) |
| 右       | *++* *--* *~* *(int)* *(float)* *(string)* *(array)* *(object)* *(bool)* *@* | [类型](http://php.net/manual/zh/language.types.php)和[递增／递减](http://php.net/manual/zh/language.operators.increment.php) |
| 无       | *instanceof*                                                 | [类型](http://php.net/manual/zh/language.types.php)          |
| 右       | *!*                                                          | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |
| 左       | *** */* *%*                                                  | [算术运算符](http://php.net/manual/zh/language.operators.arithmetic.php) |
| 左       | *+* *-* *.*                                                  | [算术运算符](http://php.net/manual/zh/language.operators.arithmetic.php)和[字符串运算符](http://php.net/manual/zh/language.operators.string.php) |
| 左       | *<<* *>>*                                                    | [位运算符](http://php.net/manual/zh/language.operators.bitwise.php) |
| 无       | *<* *<=* *>* *>=*                                            | [比较运算符](http://php.net/manual/zh/language.operators.comparison.php) |
| 无       | *==* *!=* *===* *!==* *<>* *<=>*                             | [比较运算符](http://php.net/manual/zh/language.operators.comparison.php) |
| 左       | *&*                                                          | [位运算符](http://php.net/manual/zh/language.operators.bitwise.php)和[引用](http://php.net/manual/zh/language.references.php) |
| 左       | *^*                                                          | [位运算符](http://php.net/manual/zh/language.operators.bitwise.php) |
| 左       | *\|*                                                         | [位运算符](http://php.net/manual/zh/language.operators.bitwise.php) |
| 左       | *&&*                                                         | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |
| 左       | *\|\|*                                                       | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |
| 左       | *??*                                                         | [比较运算符](http://php.net/manual/zh/language.operators.comparison.php) |
| 左       | *? :*                                                        | [ternary](http://php.net/manual/zh/language.operators.comparison.php#language.operators.comparison.ternary) |
| right    | *=* *+=* *-=* **=* **\*=* */=* *.=* *%=* *&=* *\|=* *^=* *<<=* *>>=* | [赋值运算符](http://php.net/manual/zh/language.operators.assignment.php) |
| 左       | *and*                                                        | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |
| 左       | *xor*                                                        | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |
| 左       | *or*                                                         | [逻辑运算符](http://php.net/manual/zh/language.operators.logical.php) |

> 如果想都记住是不太现实的，也没有必要。如果写的表达式很复杂，而且包含了较多的运算符，不妨多使用括号

` $a and (($b != $c) or (5 * (50 – $d)))`



注意`or`和`=`的优先级

```php
<?php
$a = false or true;
var_dump($a);
```





## PHP表达式

表达式是 PHP 最重要的基石。

在 PHP 中，几乎所写的任何东西都是一个表达式。

简单但却最精确的定义一个表达式的方式就是“任何有值的东西”。

