# Javascript 名词解释

## 语句

-   JavaScript 程序的执行单位为行（line），语句以分号结尾。一般情况下，每一行代码就是一个语句。

```javascript
var a = 1 + 3; // 初始化一个变量, 值为3
```

-   多个语句可以写在一行内。但是一般情况下一行只写一条语句。

```javascript
var a = 1 + 3;
var b = "abc"; // 可以多行, 但是需要分号
```

## 变量

-   其表示的值可以发生改变的量，叫做变量。
-   注意: name 是浏览器的保留字 , 不建议在 js 中使用

```javascript
var a; // 在这个例子中a表示一个变量，a是变量的变量名。
```

-   创建一个变量的过程叫做`变量的声明`。
-   给变量一个具体的值的过程叫做`变量的赋值`。(变量在赋值之前必须被声明)

```javascript
a = 10;
```

-   将变量的声明和赋值写在一起的方式叫做`变量的初始化`。
-   变量的声明+变量的赋值 = 变量的初始化

```javascript
var a = 10; // 初始化语句
```

-   一次声明多个变量

```javascript
var a = 1,
    b = 2,
    c = 3,
    d = 4; // 中间用逗号隔开
console.log(a); // 1;
console.log(b); // 2;
console.log(c); // 3;
console.log(d); // 4;
```

# Javascript 变量命名规则

-   JavaScript 语言的标识符对大小写敏感，所以 a 和 A 是两个不同的标识符。

```javascript
var num = 10; // num和Num不是
var Num = 20;
console.log(num); // 10
console.log(Num); // 20
```

```javascript
var num = 10; // 赋值10
var num = 20; // 又赋值20
console.log(num); // 20
console.log(num); // 20
```

-   首字母可以是任意字母以及美元符号和下划线。剩余可以是任意字母，美元符号，下划线和数字

```
aNum   FrankenStein  _My_Id  $name4 $user_address
```

-   不能使用数字来当做命名的首位。
-   不能使用 javascript 中的关键字(保留字)来命名变量

```
arguments、break、case、catch、class、const、continue  ……
```

-   name 也是关键字
-   常用命名方式：驼峰命名法(首字母小写，其余字母大写)

```javascript
var userName = 15;
console.log(userName);
```

-   给变量命名一定要给有意义的名字，不要使用类似 a、b、c 之类的无意义名字。(见名知意)

*   保留字不能用, name 不建议使用, 也是保留字
*   字母, 数字, 下划线,美元符号来组成, 但是数字不能开头
    ![](images/screenshot_1542278299152.png)
*   可以使用中文作为变量名吗(可以)

```javascript
var 帅哥 = "许竣皓";
console.log(帅哥);
```

# 如何查看变量值?

1. 控制台 console.log(变量)
1. 弹窗 alert(变量)
1. 控制台中实时查看

```javascript
// 控制台查看
var a = 1,
    b = 2,
    c = 3,
    d = 4; // 一次声明多个不同变量,逗号分开
console.log(a);
console.log(b);
console.log(c);
console.log(d);
```

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="ie=edge" />
        <title>Document</title>
    </head>
    <body>
        <script>
            // alert输出
            var userName = "China";
            alert(userName); // 弹出变量的值
        </script>
    </body>
</html>
```

```javascript
// 控制台直接返回结果
var userName = "China"; // undefined
userName; // 直接返回结果
```

# Javascript 变量类型

**_Javascript 中有六大基本数据类型，这六种数据类型也就是我们声明变量的类型。_**

1. `number` 数字类型
2. `string` 字符(串)类型
3. `boolean` 布尔类型
4. `*Array` 数组类型（不是基本数据类型）
5. `undefined`&`null` 未定义类型&空类型
6. `object` 对象类型

**_JavaScript 拥有动态类型。这意味着变量可以根据其保存的值的类型不同，显示为不同的类型。_**

```javascript
var x; // x 为 undefined类型
console.log(typeof x);
var x = 6; // x 为数字类型
console.log(typeof x);
var x = "Bill"; // x 为字符串类型
console.log(typeof x);
```

## number 数字类型

-   JavaScript 只有一种数字类型。数字可以带小数点，也可以不带：

```javascript
var x1 = 34.0; //使用小数点来写
console.log(typeof x1);
var x2 = 34; //不使用小数点来写
console.log(typeof x2);
```

-   极大或极小的数字可以通过科学计数法来书写：

```javascript
var y = 123e5; // 12300000
console.log(y);
var z = 123e-5; // 0.00123
console.log(z);
```

## string 字符(串)类型

-   字符串是存储字符（比如 "Frankenstein"）的变量。字符串可以是引号中的任意文本。
-   可以使用单引号或双引号：

```javascript
var userName = "Frankenstein";
var userName = "Ma Yun";
```

-   可以在字符串中使用引号，只要不与包围字符串的引号冲突即可：

```javascript
var answer = "Nice to meet you!";
answer = "He is called 'Frank'"; //外层是双引号，内层是单引号
answer = 'He is called "Frank"';
```

## boolean 布尔类型

-   布尔（逻辑）只能有两个值：true 或 false。

```javascript
var x=true；
var y=false；
```

-   布尔常用在条件测试中，表示真假值。

## Array 数组类型

-   数组是一组连续有序的变量的集合，数组中的变量根据数组中的下标来进行访问，数组中的变量被称为数组元素。

```javascript
// 语法：
var 数组名 = new Array(元素, 元素, 元素);
var 数组名 = [元素, 元素, 元素];
```

```javascript
var cars = new Array();
cars[0] = "Audi"; // 按下标取值并赋值
cars[1] = "BMW";
cars[2] = "BeiDouXing";
var cars = new Array("Toyota", "BMW", "volkswagen");
var cars = ["Audi", "BMW", "BeiDouXing"];
```

-   数组类型是一种特殊的对象类型。



## undefined&null 未定义类型&空类型

-   Undefined 类型表示数据类型未知或者存在类型错误。如果变量的值为 undefined，并不代表变量没有类型！

```javascript
var name;
console.log(name); //此时变量name的类型就是undefined类型
```

-   null 类型表示对象为空

```javascript
var name;
name = null；
console.log(name);  //此时name就不再是变量，而是一个对象。类型就是null类型。
```

> **_总结：undefined 类型和 null 类型在页面中表现的效果是相同的，但是 undefined 用于变量类型，而 null 用于对象类型。两者必须不能混用！！！！_**

## object 对象类型

-   对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。属性由逗号分隔：

```javascript
var person = { firstname: "Bill", lastname: "Gates", id: 5566 };
```

-   上面例子中的对象 person 有三个属性：firstname、lastname 以及 id。

```javascript
// 空格和折行无关紧要。声明可横跨多行：
var person = {
    firstname: "Bill",
    lastname: "Gates",
    id: 5566
};
```

-   对象属性有两种寻址方式（获取对象属性所对应的值的方式）：

```javascript
name = person.lastname;
name = person["lastname"];
```

# 如何显示变量类型

> typeof 用来显示变量类型

```javascript
var userName = "I love China !!!"; // 没有问题
console.log(typeof userName); // string
console.log(typeof 1.33); // number
console.log(typeof []); // 数组, 是一个特殊的对象, 所以是object
console.log(typeof {}); // 是一个对象, 所以是object
```

# js 的注释

## 什么是注释?

> 注释就是对代码的解释, 运行时直接跳过

## 注释方式有哪些?

-   单行注释
    -   `//` , 单行注释, 一般写在行尾, 解释当前行
        ![](images/screenshot_1542278336091.png)
-   多行注释
    -   `/* comment... */` 多行注释 , 可以单行可以多行, 单独写一行, 用来解释多行代码
        ![](images/screenshot_1542278351327.png)

*   多行注释也可以对文件进行注释
    ![](images/screenshot_1542278366130.png)

## 注释的作用?

1. 解释代码， 让代码易于阅读
2. 先注释， 方便修改
3. 方便排错（把最有可能出现问题的地方， 注释掉， 如果其他没有问题， 则可以定位错误）

# 排错有几种方式

1. 浏览器的控制台
2. 编辑器和 ide 的代码提示， 代码审查
3. debug

# 什么是语句?

-   一行代码就是一个语句, 用分号结束

```javascript
var a = 1;
var b = 2;
```

-   多行写一行, 需要加分号

```javascript
var a = 1;
var b = 2;
```

# 什么是代码压缩?

1. 压缩文件大小, 加快下载速度
1. 把空白行, 换行干掉, 隐藏变量名
   ![1547735106371](assets/1547735106371.png)

# 数据类型转换

## 强制数据类型转换

```javascript
var a = 1;
var b = 2;
console.log(a + b); // 3

var c = "hello";
var d = "world";
console.log(c + " " + d); // hello world(字符串连接符)
```

## 转整数

```javascript
console.log(parseInt("123")); // 123
console.log(parseInt("-123")); // -123
console.log(parseInt("+123")); // 123
console.log(parseInt("123.00")); // 123
console.log(parseInt("123元")); // 123
console.log(parseInt("hello333")); // NaN not a number
console.log(parseInt("")); // NaN not a number
console.log(parseInt("123.11元")); // 123
console.log(parseInt("helloworld")); // NaN not a number

console.log(parseInt([])); // NaN
console.log(parseInt(["1"])); // 1
console.log(parseInt(["1", "2", "3"])); // 1

console.log(parseInt("AA")); // NaN
console.log(parseInt("AA", 16)); // 170 , 第二个参数表示进制
console.log(parseInt("10", 8)); // 8
console.log(parseInt("10", 2)); // 2
console.log(parseInt("10", 10)); // 10
```
