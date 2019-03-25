# php 函数

## 定义和调用函数

```php
function fun_name($str1,$str2…$strn){
    fun_body;
}
```

## 函数间传递参数

#### 按值传递

> 形参不影响实参

```php
<?php

function square($a){
    $a = $a*$a;
    return $a;
}
$a = 3;
echo square($a); // 9
echo "\n";
echo $a; // 3
```

## 按引用传递

> 形参会影响实参

```php
<?php

function square(&$a){
    $a = $a*$a;
    return $a;
}
$a = 3;
echo square($a); // 9
echo "\n";
echo $a; // 3
```

## 默认参数

> 给参数一个默认值

```php
<?php
function add ($a,$b=1,$c=2){
    return $a+$b+$c;
}

echo add(1,2,3); // 6
echo add(1); // 4
```

## 可变参数

> 类似于 js 的`arguments`
>
> count()相当于 js 的`arr.length`

```php
<?php
function sum()
{
    $sum = 0;
    $arr = func_get_args();
    for ($i = 0; $i < count($arr); $i++) {
        $sum += $arr[$i];
    }
    return $sum;
}
echo sum(1, 2, 3);

```

## 从函数中返回值

> return 的作用是将函数的值返回给函数的调用者, 即将程序控制权返回到调用者的作用域。
>
> 如果在全局作用域内使用 return 关键字，那么将终止脚本的执行。

```php
<?php
function sum()
{
    return "hello world";
}
echo sum();
```

```php
<?php
$a = "hello world";
return;
echo $a;

```

## 变量函数

> 变量+函数==>\$a()

```php
<?php
function hello()
{
    echo 'hello world';
}

$a = 'hello';
$a();

```

# 流程控制

## 分支结构

#### 单一分支结构

if 语句

![1546852057265](images/1546852057265.png)

![1546852080316](images/1546852080316.png)

#### 双向分支结构

if else

![1546852108348](images/1546852108348.png)

![1546852127421](images/1546852127421.png)

![1546852141802](images/1546852141802.png)

#### 多项分支结构

elseif

![1546852159715](images/1546852159715.png)

![1546852191775](images/1546852191775.png)

#### switch

![1546852242844](images/1546852242844.png)

```php
<?php

$week = date("D");

if ($week === "Mon") {
    echo "星期一";
} elseif ($week === "Tue") {
    echo "星期二";
} elseif ($week === "Wed") {
    echo "星期三";
} elseif ($week === "Thu") {
    echo "星期四";
} elseif ($week === "Fri") {
    echo "星期五";
} elseif ($week === "Sat") {
    echo "星期六";
} elseif ($week === "Sun") {
    echo "星期日";
}

```

```php
<?php

$week = date('D');
switch ($week) {
    case 'Mon':echo "星期一"; break;
    case 'Tue':echo "星期二"; break;
    case 'Wed':echo "星期三"; break;
    case 'Thu':echo "星期四"; break;
    case 'Fri':echo "星期五"; break;
    case 'Sat':echo "星期六"; break;
    case 'Sun':echo "星期日"; break;
}

```

## 巢状分支结构

![1546859545218](images/1546859545218.png)

#### 循环结构

#### while

![1546875459630](images/1546875459630.png)

#### do while

![1546875483035](images/1546875483035.png)

#### for

![1546875501446](images/1546875501446.png)

#### foreach

```php
foreach (array_expression as $value)
    statement;
```

```php
foreach (array_expression as $key => $value)
    statement;
```

## 特殊的流程控制语句

#### break

终止当前循环

![1546875630897](images/1546875630897.png)

#### continue

跳过当前循环

![1546875674707](images/1546875674707.png)

#### php 跳出多重循环

```php
<?php
for ($i=0; $i < 10; $i++) {
    echo "first $i";
    echo "\n";
    for ($j=0; $j < 20; $j++) {
        echo "second $j";
        echo "\n";
        if ($j === 5) {
            break 2;
        }
    }
}
```

js 相应的解决方案

1. 标签

```javascript
outer: for (var i = 0; i < 10; i++) {
    console.log("outer i " + i);
    inter: for (var j = 0; j < 10; j++) {
        if (i > 5) {
            console.log("inner j " + j);
            break outer;
        }
    }
}
```

2. 多次 break

```javascript
var breaked = false;
for (var i = 0; i < 3; i++) {
    for (var j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            breaked = true;
            break;
        }
        console.log("i=" + i + ",j=" + j);
    }
    if (breaked) {
        break;
    }
}
```

3. 直接 return

```javascript
(function() {
    for (var i = 0; i < 3; i++) {
        for (var j = 0; j < 3; j++) {
            if (i === 1 && j === 1) {
                return;
            }
            console.log("i=" + i + ",j=" + j);
        }
    }
})();
```

# 字符串

## 单双引号的区别

单引号只能解析`\'`和`\\`

双引号可以直接解析变量和众多转义字符

## 去除字符串首尾空格和特殊字符

> 在 PHP 中提供了 trim()函数去除字符串左右两边的空格和特殊字符、
>
> ltrim()函数去除字符串左边的空格和特殊字符、
>
> rtrim()函数去除字符串右边的空格和特殊字符。

`string trim(string str [,string charlist]);`

```php
<?php
$a = "   hello world     ";
echo "'".$a."'";
echo "\n";
echo "'".trim($a)."'";
```

```php
<?php
$a = "   hello world\t\t     ";
echo "'".$a."'";
echo "\n";
echo "'".trim($a," ")."'";
```

trim()函数的参数 str 是要操作的字符串对象；参数 charlist 为可选参数，指定需要从字符串中删除哪些字符，如果不设置该参数，则所有的可选字符都将被删除。trim()函数的参数 charlist 的可选值如表

![1546921943768](images/1546921943768.png)

除了以上默认的 charlist 的可选值外，也可以在 charlist 参数中提供要去除的特殊字符。

ltrim()函数用于去除字符串左边的空格和特殊字符。

语法格式如下：

`string ltrim(string str [,string charlist]);`

```php
<?php
$a = "world hello world";

echo "'".ltrim($a,'world')."'";
```

rtrim()函数 rtrim()函数用于去除字符串右边的空格和特殊字符。语法格式如下：

`string rtrim(string str [,string charlist]);`

```php
<?php
$a = "world hello world";

echo "'".rtrim($a,'world')."'";
```

## 转义、还原字符串数据

#### 手动转义、还原字符串数据

> 数据量不大的时候使用

#### 自动转义、还原字符串数据

addslashes()函数用来为字符串 str 加入反斜线“\”。语法格式如下：

`string addslashes(string str)`

```php
<?php
$a = "I said 'I love China!'";
echo addslashes($a);
echo $a;
```

`stripslashes()`函数用来将使用`addslashes()`函数转义后的字符串 str 返回原样。语法格式如下：

`string stripslashes(string str);`

```php
<?php
$a = "I said \'I love China!\'";
echo stripcslashes($a);

```

## 获取字符串的长度

strlen()函数主要用于获取指定字符串 str 的长度。语法格式如下：

`int strlen(string str)`

```php
<?php

echo strlen("I love China");
```

```php
<?php

echo strlen("我很爱国");
```

> 友情提示: gbk 下, 一个中文占用 2 个字节, utf-8 下, 一个中文占用 3 个字节

1 字节= 8bit

1 英文 = 1 字节

字符都是一样的 `& a 中 9`

## 截取字符串

PHP 对字符串截取可以采用 PHP 的预定义函数 substr()实现。

语法格式如下：`string substr(string str, int start [, int length])`

substr()函数的参数说明如表

![1546921928587](images/1546921928587.png)

## 检索字符串

#### 使用 strstr()函数查找指定的关键字

获取一个指定字符串在另一个字符串中首次出现的位置到后者末尾的子字符串。

如果执行成功，则返回获取的子字符串（存在相匹配的字符）；

如果失败则返回 false。

语法格式如下：

`string strstr(string haystack, string needle)`

strstr()函数的参数说明如表

![1546921918016](images/1546921918016.png)

`注意本函数区分字母的大小写。`

```php
<?php
$a = "I love the people's republic of China";
var_dump(strstr($a,"C"));

```

## 使用 substr_count()函数检索子串出现的次数

获取指定字符在字符串中出现的次数。

语法格式如下：

`int substr_count(string haystack,string needle)`

参数 haystack 是指定的字符串；参数 needle 为指定的字符。

区分大小写

```php
<?php
$a = "I love the people's republic of China";
var_dump(substr_count($a,"h"));
```

## 替换字符串

#### str_ireplace()函数

使用新的字符串（子串）替换原始字符串中被指定要替换的字符串。

语法格式如下：`mixed str_ireplace(mixed search, mixed replace, mixed subject [, int &count])`

将所有在参数 subject 中出现的参数 search 以参数 replace 取代，

参数 count 表示取代字符串执行的次数。本函数不区分大小写。

str_ireplace()函数的参数说明如表

![1546921902901](images/1546921902901.png)

```php
<?php
$content="白领女子公寓，温馨街南行200 米，交通便利，亲情化专人管理，您的理想选择！";
$str="女子公寓"; //定义查询的字符串常量
echo str_ireplace($str,"<font color='#FF0000'>".$str."</font>",$content); //替换字符串为红色字体
```

#### substr_replace()函数

对指定字符串中的部分字符串进行替换。

语法格式如下：`string substr_replace(string str,string repl,int start,[int length])`

substr_replace()函数的参数说明如表

![1546921880910](images/1546921880910.png)

```php
<?php
$str = "用今日的辛勤工作，换明日的双倍回报！"; //定义字符串常量
$replace = "百倍"; //定义要替换的字符串
echo substr_replace($str, $replace, 26, 4); //替换字符串

```

## 字符串转数组

`array explode(string separator,string str [,int limit])`

```php
<?php
var_dump(explode(" ","I love china"));

```

```php
<?php
$a = "I love the people's republic of China";
var_dump(explode(" ", $a,1));

```

```php
<?php
$a = "I love the people's republic of China";
var_dump(explode(" ", $a,1)); // 数组中只有一个元素, 就是整个字符串
var_dump((array)$a);
var_dump(settype($a,'array'));
var_dump($a);
```

## 数组转字符串

implode()函数可以将数组的内容组合成一个新字符串。

语法格式如下：

`string implode(string glue, array pieces)`

参数 glue 是字符串类型，指定分隔符；

参数 pieces 是数组类型，指定要被合并的数组。

```php
<?php
$arr = [
    'I','love','China'
];
echo implode('-',$arr);
```

## 番外: 另外的字符串替换函数

```php
<?php

$str = "test";


$str5 = strtr($str, array("t" => ''));
echo '$str5: ' . $str5 . "\n";
$str6 = strtr($str, array("e" => 'www', "s" => "hhh"));
echo '$str6: ' . $str6 . "\n";
```

有两种传递参数的格式，一种是数组 k=>v 形式，一种是两个字符串的形式。



-   数组 k=>v 情况 string strtr ( string $str , array $replace_pairs )：
-   这种情况比较简单，就是把字符串中的 k 替换成 v





# 数组



## php数组vsjs数组



js的数组

```javascript
var arr = [];
arr[0] = 1;
arr[1] = 2;
arr[22] = 3;
console.log(arr);
console.log(arr.length);


```



php数组(==`别人家的数组`==)

```php
<?php

$arr = [];
$arr[] = 1;
$arr[] = 1;
$arr[] = 1;
$arr[33] = 1;
$arr[] = 1;
$arr['name'] = 1;
$arr[44] = 1;
$arr['sex'] = 1;
$arr[2] = 222;
$arr[0] = 1;
$arr[] = 1;
$arr[] = 1;
$arr[] = 1;
$arr[] = 1;
$arr[] = 1;
$arr[] = 1;
var_dump($arr);
var_dump(count($arr));
```





![1546926121949](assets/1546926121949.png)





## 数组类型

#### 索引数组

![1546926234731](assets/1546926234731.png)



#### 声明索引数组

```php
<?php

$arr = [];
$arr1 = array();
$arr2[] = 1;

var_dump($arr);
var_dump($arr1);
var_dump($arr2);
```



#### 关联数组

```php
<?php

$arr = ['name'=>'yunhe'];
$arr1 = array('name'=>'yunhe');
$arr2['name'] = 'yunhe';

var_dump($arr);
var_dump($arr1);
var_dump($arr2);
```









![1546926272314](assets/1546926272314.png)





## 输出数组

#### `var_dump`

#### `print_r`



```php

<?php

$arr = ['name'=>'yunhe'];
$arr1 = array('name'=>'yunhe');


var_dump($arr);
print_r($arr1);

```





## 遍历数组

#### `foreach`

```php
<?php

$arr = [
    'name'=>'yunhe',
    'name0'=>'yunhe0',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

foreach ($arr as $key => $value) {
    echo "$key ==> $value";
    echo "\n";
}
```



#### `for`

> 只能遍历索引数组



## 数组的键值操作

#### `array_values()`



关联转索引

```php
<?php

$arr = [
    'name'=>'yunhe',
    'name0'=>'yunhe0',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(array_values($arr)); // 关联转索引
```





#### `array_keys()`

```php
<?php

$arr = [
    'name'=>'yunhe',
    'name0'=>'yunhe0',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(array_keys($arr)); // 关联转索引
```



![1546928542404](assets/1546928542404.png)

> 取所有的key
>
> 第二个参数, 根据value找key
>
> 第三个参数, true代表全等, 默认false

#### `in_array()`

```php
<?php

$arr = [
    'name'=>'111',
    'name0'=>111,
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(in_array('111',$arr)); 


```

> 第三个参数表示全等, 默认false, 不需要全等



![1546928614514](assets/1546928614514.png)



#### `array_search()`

> 搜索给定的值, 存在返回键名

```php
<?php

$arr = [
    'name'=>'111',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(array_search(111,$arr,true)); 


```

> 第三个参数表示全等, 默认false, 不需要全等

#### `array_key_exists()`

> 键名是否存在于数组之中

```php
<?php

$arr = [
    'name'=>'111',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(array_key_exists('name',$arr)); 


```



#### `array_flip()`

> 数组键值翻转(数组不会变)

```php
<?php

$arr = [
    'name'=>'111',
    'name1'=>'yunhe1',
    'name2'=>'yunhe2',
    'name3'=>'yunhe3',
    'name4'=>'yunhe4',
    'name5'=>'yunhe5'
];

var_dump(array_flip($arr)); 
var_dump($arr);
```



#### `array_reverse()`

> 数组值翻转(多用于索引数组)

```php
<?php

$arr = [
'111',
'yunhe1',
'yunhe2',
'yunhe3',
'yunhe4',
'yunhe5'
];

var_dump(array_reverse($arr)); 
var_dump($arr);


```





## 统计元素个数

#### `count()`



![1546927421194](assets/1546927421194.png)

```php
<?php

$arr = [
    1, 2, 3, [1, 2, 3],
];

echo count($arr,COUNT_RECURSIVE);

```



## 统计数组中所有值出现的次数

#### `array_count_values()`



```php
<?php

$arr = [
    1, 2, 3, 1,2,3,3
];

var_dump(array_count_values($arr));


```








## 获取数组中最后一个元素

#### `array_pop` 删除并返回最后一个元素

![1546927786850](assets/1546927786850.png)

```php
<?php

$arr = [
    1, 2, 3, 1,2,3,3
];

var_dump(array_pop($arr));


```



## 数组中添加元素

#### `array_push` 插入最后

![1546927857747](assets/1546927857747.png)



```php
<?php

$arr = [
    1, 2, 3, 1,2,3,3
];

var_dump(array_push($arr,4));

var_dump($arr);
```



## 删除数组中重复的元素

#### `array_unique()`





![1546928048018](assets/1546928048018.png)

```php
<?php

$arr = [
    1, 2, 3, 4, 5, 5, 5, 6,
];


print_r(array_unique($arr));
```



```php
<?php

$arr = [
    1, 2, 3, 1,2,3,3
];

var_dump(array_unique($arr));

var_dump($arr);
```

