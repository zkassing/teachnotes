# JSON

**JSON**(JavaScript Object Notation) 是一种轻量级的数据交换格式。 易于人阅读和编写。同时也易于机器解析和生成。

JSON 采用完全独立于语言的文本格式，但是也使用了类似于 C 语言家族的习惯（包括 C, C++, C#, Java, JavaScript, Perl, Python 等）。 这些特性使 JSON 成为理想的数据交换语言。

**JSON：JavaScript 对象表示法（JavaScript Object Notation）。**

**JSON 是存储和交换文本信息的语法。类似 XML。**

**JSON 比 XML 更小、更快，更易解析。**

JSON 建构于两种结构：

-   “名称/值”对的集合（A collection of name/value pairs）。不同的语言中，它被理解为*对象（object）*，纪录（record），结构（struct），字典（dictionary），哈希表（hash table），有键列表（keyed list），或者关联数组 （associative array）。
-   值的有序列表（An ordered list of values）。在大部分语言中，它被理解为数组（array）。

这些都是常见的数据结构。事实上大部分现代计算机语言都以某种形式支持它们。这使得一种数据格式在同样基于这些结构的编程语言之间交换成为可能。

JSON 具有以下这些形式：

对象是一个无序的“‘名称/值’对”集合。一个对象以“{”（左括号）开始，“}”（右括号）结束。每个“名称”后跟一个“:”（冒号）；“‘名称/值’ 对”之间使用“,”（逗号）分隔。

![img](images/object.gif)

数组是值（value）的有序集合。一个数组以“[”（左中括号）开始，“]”（右中括号）结束。值之间使用“,”（逗号）分隔。

![img](images/array.gif)

值（_value_）可以是双引号括起来的字符串（_string_）、数值(number)、`true`、`false`、 `null`、对象（object）或者数组（array）。这些结构可以嵌套。

![img](images/value.gif)

字符串（_string_）是由双引号包围的任意数量 Unicode 字符的集合，使用反斜线转义。一个字符（character）即一个单独的字符串（character string）。

字符串（_string_）与 C 或者 Java 的字符串非常相似。

![img](images/string.gif)

数值（_number_）也与 C 或者 Java 的数值非常相似。除去未曾使用的八进制与十六进制格式。除去一些编码细节。

![img](images/number.gif)

空白可以加入到任何符号之间。 以下描述了完整的语言。

## 实例

```javascript
{
	"employees": [
		{ "firstName":"Bill" , "lastName":"Gates" },
		{ "firstName":"George" , "lastName":"Bush" },
		{ "firstName":"Thomas" , "lastName":"Carter" }
	]
}
```

这个 employee 对象是包含 3 个员工记录（对象）的数组。

## JSON 语法规则

JSON 语法是 JavaScript 对象表示法语法的子集。

-   数据在名称/值对中
-   数据由逗号分隔
-   花括号保存对象
-   方括号保存数组

## JSON 名称/值对

JSON 数据的书写格式是：名称/值对。

名称/值对包括字段名称（在双引号中），后面写一个冒号，然后是值：

```
"firstName" : "John"
```

这很容易理解，等价于这条 JavaScript 语句：

```
firstName = "John"
```

## JSON 值

JSON 值可以是：

-   数字（整数或浮点数）
-   字符串（在双引号中）
-   逻辑值（true 或 false）
-   数组（在方括号中）
-   对象（在花括号中）
-   null

## JSON 对象

JSON 对象在花括号中书写：

对象可以包含多个名称/值对：

```
{ "firstName":"John" , "lastName":"Doe" }
```

这一点也容易理解，与这条 JavaScript 语句等价：

```
firstName = "John"
lastName = "Doe"
```

## JSON 数组

JSON 数组在方括号中书写：

数组可包含多个对象：

```javascript
{
	"employees": [
		{ "firstName":"John" , "lastName":"Doe" },
		{ "firstName":"Anna" , "lastName":"Smith" },
		{ "firstName":"Peter" , "lastName":"Jones" }
	]
}
```

在上面的例子中，对象 "employees" 是包含三个对象的数组。每个对象代表一条关于某人（有姓和名）的记录。

## JSON 使用 JavaScript 语法

因为 JSON 使用 JavaScript 语法，所以无需额外的软件就能处理 JavaScript 中的 JSON。

通过 JavaScript，您可以创建一个对象数组，并像这样进行赋值：

### 例子

```
var employees = [
{ "firstName":"Bill" , "lastName":"Gates" },
{ "firstName":"George" , "lastName":"Bush" },
{ "firstName":"Thomas" , "lastName": "Carter" }
];
```

可以像这样访问 JavaScript 对象数组中的第一项：

```
employees[0].lastName;
```

返回的内容是：

```
Gates
```

可以像这样修改数据：

```
employees[0].lastName = "Jobs";
```

**JSON**对象包含两个方法: 用于解析 [JavaScript Object Notation](111)` 方法。除了这两个方法, JSON 这个对象本身并没有其他作用

-   [`JSON.parse()`](111)

        	解析JSON字符串并返回对应的值

-   [`JSON.stringify()`](111)

        	返回与指定值对应的JSON字符串

### JSON.parse() 返回值

[`Object`](111)类型, 对应给定 JSON 文本的对象/值。

### 异常

若传入的字符串不符合 JSON 规范，则会抛出 [`SyntaxError`](111) 异常。

### 使用 `JSON.parse()`

```js
JSON.parse("{}"); // {}
JSON.parse("true"); // true
JSON.parse('"foo"'); // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse("null"); // null
JSON.parse("1"); //  1
```

### `JSON.parse()` 不允许用逗号作为结尾

```js
// both will throw a SyntaxError
JSON.parse("[1, 2, 3, 4, ]");
JSON.parse('{"foo" : 1, }');
```

### `JSON.stringify()` 方法是将一个 JavaScript 值(对象或者数组)转换为一个 JSON 字符串
