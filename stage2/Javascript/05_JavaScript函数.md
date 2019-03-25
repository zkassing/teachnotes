# 函数

## 什么是函数?

-   函数就是执行指定功能的代码段

```javascript
function helloWorld() {
    console.log("hello world !!!");
}

helloWorld(); // 输出helloWorld
```

## 函数的命名规范

-   动词+名词
-   命名规范和变量一致
    1. 区分大小写
    2. 不能数字开头
    3. 不能保留字
    4. 不能空格

## 如何定义一个函数

```javascript
function 函数名(参数) {
    代码段;
}
```

```javascript
var 函数名 = function(参数) {
    代码段;
};
```

```javascript
// plusNumber() = a+b
function plusNumber() {
    var a = 1;
    var b = 2;
    return a + b;
}
```

```javascript
// plusNumber() = a+b
var plusNumber = function() {
    var a = 1;
    var b = 2;
    return a + b;
};
```

## 函数的运行, 需要调用

```javascript
// 单纯定义是没有结果的
function helloWorld() {
    console.log("hello world !!!");
}
```

## 什么是函数的参数

-   函数中用到的变量
-   可以让函数变得更加灵活

```javascript
function printSomething(sth) {
    console.log(sth);
}

printSomething("hello world"); // hello world
printSomething("hello USA"); // hello USA
```

## 什么是函数的返回值?

-   返回函数运行的结果

### 没有返回值的情况

```javascript
function plusNumber() {
    var a = 1;
    var b = 2;
    console.log(a + b);
}

plusNumber(); // 3
```

### 没有返回值会返回 `undefined`

```javascript
function plusNumber() {
    var a = 1;
    var b = 2;
    // console.log(a+b);
    a + b;
}

plusNumber(); // 3
console.log(plusNumber()); // undefined
```

### 函数和返回值的关系, 相当于变量和变量值的关系

```javascript
// plusNumber() = a+b
function plusNumber() {
    var a = 1;
    var b = 2;
    return a + b;
}

console.log(plusNumber()); // 3
```

### 返回值需要被变量接收

```javascript
function plusNumber() {
    var a = 1;
    var b = 2;
    return a + b;
}

plusNumber(); // 没有结果
```

```javascript
function plusNumber() {
    var a = 1;
    var b = 2;
    return a + b;
}
var result = plusNumber();
console.log(plusNumber()); // 3
```

## 函数传参

```javascript
// plusNumber() = a+b
function plusNumber(a, b) {
    return a + b;
}
var res = plusNumber(3, 4);

console.log(res); // 7
```

-   传参, 就是传变量

```javascript
// plusNumber() = a+b
function plusNumber(a, b) {
    return a + b;
}

var first = 33;
var second = 4;
var res = plusNumber(first, second);

console.log(res); // 37
```

## 使用 vscode 查看函数解释(把鼠标移到函数名称上, 即可显示)

![](images/screenshot_1542275264989.png)

## 默认参数

-   如果不传值, 参数也可以保证函数运算时, 有值可用, 可以提交代码的健壮性

```javascript
function plusNum(a = 1, b = 2) {
    return a + b;
}

console.log(plusNum()); // 3
```

-   推荐使用下面这一种

```javascript
function plusNum(a, b) {
    var a = a || 1;
    var b = b || 2;
    return a + b;
}

console.log(plusNum()); // 3
```

