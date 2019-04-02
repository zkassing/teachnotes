[toc]

# 数组属性

## 什么是数组?

-   数据类型之一, 表示一组数据
-   array ==> 数组

## 如何声明数组

```javascript
var arr = new Array();
var arr = [];
```

## 如何增加元素

```javascript
var arr = [];
arr[0] = 1;
arr[1] = 2;
```

## 如何获取元素

```javascript
var arr = [1, 2, 3, 4];
arr[2]; // 3
arr[2] = 5; // 数组会变成[1,2,5,4]
```

## 如何获取数组长度

```javascript
var arr = [1, 2, 3, 4];
console.log(arr.length); // 4
```

-   `length` 是一个对象的属性,所谓属性, 我们现在叫做变量

```javascript
var arr = [1, 2, 3, 4];
console.log(arr.length);
arr[4] = 100;
console.log(arr.length); // 5
arr[6] = 100;
console.log(arr.length); // 7
```

## 对象

```javascript
var obj = {
    name: "China",
    sex: "female"
};

console.log(obj.name); // China
obj.name = "USA";
console.log(obj.name); // USA
```

-   索引可以不加引号

```javascript
var obj = {
    name: "China",
    sex: "female"
};

console.log(obj.name); // China
obj.name = "USA";
console.log(obj.name); // USA
```

## 获取数组长度的两种方式

```javascript
var arr = [1, 2, 3, 4];
console.log(arr["length"]); // 4
arr[4] = 100;
console.log(arr["length"]); // 5
arr[6] = 100;
console.log(arr["length"]); // 7
```

```javascript
var arr = [1, 2, 3, 4];
console.log(arr.length); // 4
arr[4] = 100;
console.log(arr.length); // 5
arr[6] = 100;
console.log(arr.length); // 7
```

# 数组方法

## concat() `合并`

-   连接两个或更多的数组，并返回结果。
-   `arrayObject.concat(arrayX,arrayX,......,arrayX)`

**_注意使用方式_**

首先是错误示范...

```javascript
var arr1 = ["I", "love", "China"];
var arr2 = ["!", "!", "!"];

console.log(concat(arr1, arr2)); // concat is not defined 没有定义, 因为是对象方法, 不是自定义函数
```

下面是正确的...

```javascript
var arr1 = ["I", "love", "China"];
var arr2 = ["!", "!", "!"];

console.log(arr1.concat(arr2)); // 把arr1和arr2 合并了, arr1的内容在前, arr2的内容在后
console.log(arr2.concat(arr1)); // 把arr1和arr2 合并了, arr2的内容在前, arr1的内容在后
```

```javascript
var arr1 = ["I", "love", "China"];
var arr2 = ["!", "!", "!"];

var res = arr1.concat(arr2); // 声明一个变量接收方法的返回值
console.log(res); // 输出变量
```

## join() `转换`

-   把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。
-   `arrayObject.join(separator)`

### 什么是 separator? 分隔符

-   能起到分割作用的符号, 都可以作为分隔符, 可以起到美观的效果, 易于识别

```javascript
/* 分隔符的使用, 本质上, 数组转字符串 */
var arr1 = ["I", "love", "China"];
var arr2 = ["!", "!", "!"];

var res = arr1.join(",");
var res2 = arr1.join("-");
var res3 = arr1.join("");
var res4 = arr1.join(" ");

console.log(res); // I,love,China
console.log(res2); // I-love-China
console.log(res3); // IloveChina
console.log(res4); // I love China
```

## pop() `删除`

-   删除并返回数组的最后一个元素
-   `arrayObject.pop()`

```javascript
/* 分隔符的使用, 本质上, 数组转字符串 */
var arr1 = ["I", "love", "China", "!", "!", "!"];

var res = arr1.pop();
console.log(res); // !
res = arr1.pop();
console.log(res); // !
res = arr1.pop();
console.log(res); // !
res = arr1.pop();
console.log(res); // China
res = arr1.pop();
console.log(res); // love
res = arr1.pop();
console.log(res); // I
res = arr1.pop();
console.log(res); // undefined
```

```javascript
// 删除之后, 数组会改变
var arr = ["I", "Love", "China", "!", "!", "!"];
console.log(arr.pop()); // !
console.log(arr.pop()); // !
console.log(arr); // [ 'I', 'Love', 'China', '!' ]
```

## push() `添加`

-   向数组的末尾添加一个或更多元素，并返回新的长度。
-   `arrayObject.push(newelement1,newelement2,....,newelementX)`

```javascript
/* push 结尾追加元素, 返回长度 */
var arr1 = ["I", "love", "China"];
var res = arr1.push("!");
console.log(res); // 4
res = arr1.push("!");
console.log(res); // 5
console.log(arr1); // [ 'I', 'love', 'China', '!', '!' ]
```

## reverse() `排序`

-   颠倒数组中元素的顺序。
-   arrayObject.reverse()

```javascript
var arr = ["I", "Love", "China", "!", "!", "!"];
var res = arr.reverse();
console.log(res); // [ '!', '!', '!', 'China', 'Love', 'I' ] 顺序颠倒
```

## shift() `删除`

-   删除并返回数组的第一个元素
-   arrayObject.shift()

```javascript
var arr = [1, 2, 3, 4, 5, 6, 7, 8];
console.log(arr.shift()); // 1
console.log(arr);
console.log(arr.shift()); // 2
console.log(arr);
console.log(arr.shift()); // 3
console.log(arr);
console.log(arr.shift()); // 4
console.log(arr);
console.log(arr.shift()); // 5
console.log(arr);
console.log(arr.shift()); // 6
console.log(arr);
console.log(arr.shift()); // 7
console.log(arr);
console.log(arr.shift()); // 8
console.log(arr);
console.log(arr.shift()); // undefined
console.log(arr);
console.log(arr.shift()); // undefined
console.log(arr);
```

## unshift() `添加`

-   向数组的开头添加一个或更多元素，并返回新的长度。
-   arrayObject.unshift(newelement1,newelement2,....,newelementX)

```javascript
var arr = [];
console.log(arr.unshift(1)); // 1
console.log(arr); // [ 1 ]
console.log(arr.unshift(1, 2, 3, 4)); // 5
console.log(arr); // [ 1, 2, 3, 4, 1 ]
```

## slice() `查询`

-   从某个已有的数组返回选定的元素
-   arrayObject.slice(start,end)

```javascript
var arr = ["I", "love", "China", "!"];
console.log(arr.slice(0, 2)); // [ 'I', 'love' ]
```

-   负数是倒(四声)数的意思

```javascript
var arr = ["I", "love", "China", "!"];
console.log(arr.slice(0, -1)); // [ 'I', 'love', 'China' ]
```

-   切片不影响原数组, 因为本质是查询

```javascript
var arr = ["I", "love", "China", "!"];
console.log(arr.slice(0, -1)); // [ 'I', 'love', 'China' ]
console.log(arr); // [ 'I', 'love', 'China', '!' ]
```

```javascript
var arr = ["I", "love", "China", "!"];
// 如果没有end, 默认到结束
console.log(arr.slice(1)); // [ 'love', 'China', '!' ]
console.log(arr); // [ 'I', 'love', 'China', '!' ]
```

## sort() `排序`

-   对数组的元素进行排序, 注意`支持自定义函数`
-   arrayObject.sort(sortby)

```javascript
var arr = [3, 2, 5, 9, 11, 8]; // 当成字符串来排序了
// var arr = ['3','2','5','9','11','8'];
console.log(arr.sort()); // [ 11, 2, 3, 5, 8, 9 ]
```

```javascript
function sortNumber(a, b) {
    return a - b;
}

var arr = [3, 2, 5, 9, 11, 8];

console.log(arr.sort(sortNumber)); // [ 2, 3, 5, 8, 9, 11 ];
```

## splice() `修改`

-   删除元素，并向数组添加新元素。
-   arrayObject.splice(index,howmany,item1,.....,itemX)

```javascript
var arr = ["I", "love", "China", "!"];

var res = arr.splice(0, 3);

console.log(res); // [ 'I', 'love', 'China' ]
console.log(arr); // [ '!' ]
```

```javascript
var arr = ["I", "love", "China", "!"];

var res = arr.splice(0, 3, "hello", "world");

console.log(res); // 删掉的返回回来
console.log(arr); // [ 'hello', 'world', '!' ], 删了前三个, 替换了两个
```
