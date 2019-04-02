# 一元操作符

## 什么是一元运算符?

> 只能操作一个值的操作符叫做一元操作符

#### 递增和递减操作符

```javascript
var age = 29;
++age;
```

```javascript
var age = 29;
age = age + 1;
```

```javascript
var age = 29;
--age;
```

```javascript
var age = 29;
var anotherAge = --age + 2;
console.log(age);
console.log(anotherAge);
```

```javascript
var num1 = 2;
var num2 = 20;
var num3 = --num1 + num2;
var num4 = num1 + num2;
```

```javascript
var a = 1;
console.log(++a); // 2
console.log(a++); // 2
console.log(a); // 3

// console.log(a++); 相当于下面的代码
console.log(a); // 3
a = a + 1;
```

```javascript
var a = 10;
console.log(--a); // 9
console.log(a); // 9
console.log(a--); // 9
console.log(a); // 8
```

```javascript
var age = 29;
var anotherAge = --age + 2;
console.log(age); // 28
console.log(anotherAge); // 30
```

```javascript
var age = 29;
// var anotherAge = age-- + 2;
var anotherAge = age + 2;
age = age - 1;
console.log(age); // 28
console.log(anotherAge); // 31
```

后置型递增和递减操作符的语法不变（仍然分别是 ++ 和 -- ），只不过要放在变量的后面而不是前面。
后置递增和递减与前置递增和递减有一个非常重要的区别，即递增和递减操作是在包含它们的语句被求值之后才执行的。这个区别在某些情况下不是什么问题，例如：

```javascript
var age = 29;
age++;
```

把递增操作符放在变量后面并不会改变语句的结果，因为递增是这条语句的唯一操作。但是，当语
句中还包含其他操作时，上述区别就会非常明显了。

```javascript
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2;
var num4 = num1 + num2;
```

```javascript
var num1 = 2;
var num2 = 20;
var num5 = 12;

var num3 = ++num5 - num1-- + num2;
var num4 = num1 + num2;

console.log(num1); // 1
console.log(num2); // 20
console.log(num3); // 31
console.log(num4); // 21
```

所有这 4 个操作符对任何值都适用，也就是它们不仅适用于整数，还可以用于字符串、布尔值、浮点数值和对象。在应用于不同的值时，递增和递减操作符遵循下列规则。

#### 在应用于一个包含有效数字字符的字符串时，先将其转换为数字值，再执行加减 1 的操作。字符串变量变成数值变量。

```javascript
var num1 = "123hello";
console.log(num1++); // NaN
var num1 = "123";
console.log(num1++); // 123
console.log(++num1); // 125
```

#### 在应用于一个不包含有效数字字符的字符串时，将变量的值设置为 NaN, 字符串变量变成数值变量。

```javascript
var num1 = "hello";
console.log(num1++); // NaN
```

```javascript
var num1 = "hello";
console.log(num1++); // NaN
console.log(num1); // NaN
console.log(typeof num1); // number
```

#### 在应用于布尔值 false 时，先将其转换为 0 再执行加减 1 的操作。布尔值变量变成数值变量。

#### 在应用于布尔值 true 时，先将其转换为 1 再执行加减 1 的操作。布尔值变量变成数值变量。

```javascript
var a = true;
console.log(a++); // 1
console.log(++a); // 3

console.log(typeof a); // number
```

```javascript
var a = false;
console.log(a++); // 0
console.log(++a); // 2

console.log(typeof a); // number
```

#### 在应用于浮点数值时，执行加减 1 的操作。

```javascript
var a = 1.11;
console.log(a++); // 1.11
console.log(++a); // 3.1100000000000003

console.log(typeof a); // number
```

#### 在应用于对象时，先调用对象的 valueOf() 方法以取得一个可供操作的值。然后对该值应用前述规则。如果结果是 NaN ，则在调用 toString() 方法后再应用前述规则。对象变量变成数值变量。

```javascript
var a = [];
console.log(a++); // 0
console.log(++a); // 2

console.log(typeof a); // number

var b = {};
console.log(b++); // NaN
console.log(++b); // NaN

console.log(typeof b); // number
```

```javascript
var s1 = "2";
var s2 = "z";
var b = false;
var f = 1.1;
var o = {
    valueOf: function() {
        return -1;
    }
};
s1++;
s2++;
b++;
f--;
o--;

// console.log(s1); //3
// console.log(s2); // NaN
// console.log(b); // 1
// console.log(f); // 0.10000000000000009
console.log(o); //-2
```

2. 一元加和减操作符

```javascript
var num = 25;
num = +num;
```

不过，在对非数值应用一元加操作符时，该操作符会像 Number() 转型函数一样对这个值执行转换。
换句话说，布尔值 false 和 true 将被转换为 0 和 1，字符串值会被按照一组特殊的规则进行解析，而
对象是先调用它们的 valueOf() 和（或） toString() 方法，再转换得到的值。
下面的例子展示了对不同数据类型应用一元加操作符的结果：

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = {
    valueOf: function() {
        return -1;
    }
};
s1 = +s1; // 值变成数值 1
s2 = +s2; // 值变成数值 1.1
s3 = +s3; // 值变成 NaN
b = +b; // 值变成数值 0
f = +f; // 值未变，仍然是 1.1
o = +o; // 值变成数值-1
```

一元减操作符主要用于表示负数，例如将 1 转换成-1

```javascript
var num = 25;
num = -num; // 变成了-25
```

在将一元减操作符应用于数值时，该值会变成负数。而当应用于非数值时，一元减操作符遵循与一元加操作符相同的规则，最后再将得到的数值转换为负数，

```javascript
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = {
    valueOf: function() {
        return -1;
    }
};
s1 = +s1;
s2 = +s2;
s3 = +s3;
b = +b;
f = +f;
o = +o;

console.log(s1); // 1
console.log(s2); // 1.1
console.log(s3); // NaN
console.log(b); // 0
console.log(f); // 1.1
console.log(o); // -1
```

# 位操作符(不讲...)pass

# 布尔操作符

在一门编程语言中，布尔操作符的重要性堪比相等操作符。如果没有测试两个值关系的能力，那么诸如 if...else 和循环之类的语句就不会有用武之地了。
布尔操作符一共有 3 个：非（NOT）、与/且（AND） 和或（OR）。

## 逻辑非

逻辑非操作符由一个叹号（！）表示，可以应用于 ECMAScript 中的任何值。无论这个值是什么数据类型，这个操作符都会返回一个布尔值。
逻辑非操作符首先会将它的操作数转换为一个布尔值，然后再对其求反。也就是说，逻辑非操作符遵循下列规则：

#### 如果操作数是一个对象，返回 false ；

#### 如果操作数是一个空字符串，返回 true ；

```javascript
var a = {};
console.log(!a); // false
var b = "";
console.log(!b); // true
```

#### 如果操作数是一个非空字符串，返回 false ；

```javascript
var b = "the quick brown fox jumps over the lazy dog";
console.log(!b); // false
```

#### 如果操作数是数值 0，返回 true ；

```javascript
console.log(!0); // true

console.log(Boolean(0)); // false
```

#### 如果操作数是任意非 0 数值（包括 Infinity ），返回 false ；

```javascript
console.log(!123123); // false
console.log(Boolean(123123)); // true

console.log(!1.7976931348623157e30899); // false infinity
```

#### 如果操作数是 null ，返回 true ；

```javascript
console.log(!null); // true
console.log(Boolean(null)); // false
```

#### 如果操作数是 NaN ，返回 true ；

```javascript
console.log(!NaN); // true
console.log(Boolean(NaN)); // false
```

#### 如果操作数是 undefined ，返回 true 。

```javascript
console.log(!undefined); // true
console.log(Boolean(undefined)); // false
```

```javascript
console.log(!false); // true
console.log(!"blue"); // false
console.log(!0); // true
console.log(!NaN); // true
console.log(!""); // true
console.log(!12345); // false
```

逻辑非操作符也可以用于将一个值转换为与其对应的布尔值。而同时使用两个逻辑非操作符，实际上就会模拟 Boolean() 转型函数的行为。
其中，第一个逻辑非操作会基于无论什么操作数返回一个布尔值，而第二个逻辑非操作则对该布尔值求反，于是就得到了这个值真正对应的布尔值。当然，最终结果与对这个值使用 Boolean() 函数相同

```javascript
console.log(!!"blue"); // true
console.log(!!0); // false
console.log(!!NaN); // false
console.log(!!""); // false
console.log(!!12345); // true
```

## 逻辑与

> 两个真, 才为真. 第一个错了,就不往下跑了, 输出第一个;若第一个正确, 则不论第二个正确与否, 输出第二个.

逻辑与操作符由两个和号（ && ）表示，有两个操作数，如下面的例子所示：

```javascript
var result = true && false;
```

逻辑与的真值表如下：

| 第一个操作数 | 第二个操作数 | 结 果 |
| ------------ | ------------ | ----- |
| true         | true         | true  |
| true         | false        | false |
| false        | true         | false |
| false        | false        | false |

逻辑与操作可以应用于任何类型的操作数，而不仅仅是布尔值。在有一个操作数不是布尔值的情况下，逻辑与操作就不一定返回布尔值；此时，它遵循下列规则：

#### 如果第一个操作数是对象，则返回第二个操作数；

```javascript
var res = {} && "hello";
console.log(res); // hello
```

#### 如果第二个操作数是对象，则只有在第一个操作数的求值结果为 true 的情况下才会返回该对象；

```javascript
var res = true && {};
console.log(res); // {}
var res1 = false && {};
console.log(res1); // false
var res2 = "hello" && {};
console.log(Boolean("hello")); // true
console.log(res2); // {}
```

```javascript
var res3 = "" && {};
console.log(Boolean("")); // false

console.log(res3); // ""
```

#### 如果两个操作数都是对象，则返回第二个操作数；

```javascript
console.log({ sex: "female" } && { age: 17 }); // { age: 17 }
```

1. 如果有一个操作数是 null,一个平常值 ，则返回 null ；
1. 如果有一个操作数是 undefined,一个平常值 ，则返回 undefined 。
1. 如果有一个操作数是 NaN,一个平常值 ，则返回 NaN 。

```javascript
console.log(Boolean(null)); // false
console.log(null && { age: 17 }); // null
console.log(Boolean(undefined)); // false
console.log(undefined && { age: 17 }); // undefined
```

```javascript
console.log(Boolean(NaN)); // false
console.log(NaN && { age: 17 }); // NaN
```

逻辑与操作属于短路操作，即如果第一个操作数能够决定结果，那么就不会再对第二个操作数求值。
对于逻辑与操作而言，如果第一个操作数是 false ，则无论第二个操作数是什么值，结果都不再可能是 true 了

```javascript
var found = true;
var result = found && someUndefinedVariable;
console.log(result); // ReferenceError: someUndefinedVariable is not defined
```

```javascript
var found = false;
var result = found && someUndefinedVariable;
console.log(result); // false
```

## 逻辑或

逻辑或操作符由两个竖线符号（ || ）表示，有两个操作数，如下面的例子所示：

```javascript
var result = true || false;
```

逻辑或的真值表如下：

| 第一个操作数 | 第二个操作数 | 结 果 |
| ------------ | ------------ | ----- |
| True         | true         | true  |
| True         | false        | true  |
| false        | true         | true  |
| false        | false        | false |

与逻辑与操作相似，如果有一个操作数不是布尔值，逻辑或也不一定返回布尔值；此时，它遵循下列规则：

#### 如果第一个操作数是对象，则返回第一个操作数

```javascript
console.log({} || "1123"); // {}
```

#### 如果第一个操作数的求值结果为 false ，则返回第二个操作数；

```javascript
console.log(false || "1123"); // 1123
```

#### 如果两个操作数都是对象，则返回第一个操作数；

```javascript
console.log({ sex: "female" } || { age: 17 }); // { sex: 'female' }
```

#### 如果两个操作数都是 null ，则返回 null ；

```javascript
console.log(null || null); // null
```

#### 如果两个操作数都是 NaN ，则返回 NaN ；

#### 如果两个操作数都是 undefined ，则返回 undefined 。

```javascript
console.log(null || null); // null
console.log(undefined || undefined); // undefined
console.log(NaN || NaN); // NaN

console.log(undefined || null); // null
```

与逻辑与操作符相似，逻辑或操作符也是短路操作符。也就是说，如果第一个操作数的求值结果为
true ，就不会对第二个操作数求值了。下面看一个例子：

```javascript
var found = true;
var result = found || someUndefinedVariable;
console.log(result);
```

```javascript
var found = false;
var result = found || someUndefinedVariable;
console.log(result);
```

我们可以利用逻辑或的这一行为来避免为变量赋 null 或 undefined 值。例如：
var myObject = preferredObject || backupObject;
在这个例子中，变量 myObject 将被赋予等号后面两个值中的一个。变量 preferredObject 中包含优先赋给变量 myObject 的值，变量 backupObject 负责在 preferredObject 中不包含有效值的情况下提供后备值。如果 preferredObject 的值不是 null ，那么它的值将被赋给 myObject ；如果是 null ，则将 backupObject 的值赋给 myObject 。ECMAScript 程序的赋值语句经常会使用这种模式

```javascript
var preferredObject, backupObject;
preferredObject = "";
backupObject = "USA";
var myObject = preferredObject || backupObject;

console.log(myObject); // USA
```

# 乘性操作符

ECMAScript 定义了 3 个乘性操作符：乘法、除法和求模。
如果参与乘性计算的某个操作数不是数值，后台会先使用 Number() 转型函数将其转换为数值。
也就是说，空字符串将被当作 0，布尔值 true 将被当作 1。

## 乘法

乘法操作符由一个星号（ \* ）表示，用于计算两个数值的乘积。

```javascript
var result = 34 * 56;
```

在处理特殊值的情况下，乘法操作符遵循下列特殊的规则：

#### 如果操作数都是数值，执行常规的乘法计算，即两个正数或两个负数相乘的结果还是正数，而如果只有一个操作数有符号，那么结果就是负数。如果乘积超过了 ECMAScript 数值的表示范围，则返回 Infinity 或 -Infinity ；

```javascript
var a = Number.MAX_VALUE + 100;
var b = Number.MAX_VALUE + 1001;

console.log(a * b); // Infinity
console.log(a * -b); // -Infinity
```

#### 如果有一个操作数是 NaN ，则结果是 NaN ；

```javascript
console.log(NaN * 100); // NaN
console.log(NaN * NaN); // NaN
console.log(NaN - NaN); // NaN
console.log(NaN + NaN); // NaN
```

#### 如果是 Infinity 与 0 相乘，则结果是 NaN ；

```javascript
console.log(Number.MAX_VALUE * 100 * 0); // NaN

console.log(Number.MAX_VALUE * 10); // Infinity
```

#### 如果是 Infinity 与非 0 数值相乘，则结果是 Infinity 或 -Infinity ，取决于有符号操作数的符号；

```javascript
console.log(Number.MAX_VALUE * 10 * -1); // -Infinity
console.log(Number.MAX_VALUE * 10 * 10); // Infinity
```

#### 如果是 Infinity 与 Infinity 相乘，则结果是 Infinity ；

```javascript
console.log(Number.MAX_VALUE * 10 * (Number.MAX_VALUE * 10)); // Infinity
console.log(Number.MAX_VALUE * 10 + Number.MAX_VALUE * 10); // Infinity
console.log(Number.MAX_VALUE * 10 - Number.MAX_VALUE * 10); // NaN
console.log((Number.MAX_VALUE * 10) / (Number.MAX_VALUE * 10)); // NaN
```

#### 如果有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的规则。

```javascript
console.log([] * 100); // 0
console.log({} * 100); // NaN

console.log(Number([1, 2, 3])); // NaN
console.log([1, 2, 3] * 100); // NaN
```

#### 如果是 boolean 值, 会转成 0 或者 1, true==>1, false==>0

## 除法

除法操作符由一个斜线符号（/）表示，执行第二个操作数除第一个操作数的计算

```Javascript
var result = 66 / 11;
```

与乘法操作符类似，除法操作符对特殊的值也有特殊的处理规则。这些规则如下：

#### 如果操作数都是数值，执行常规的除法计算，即两个正数或两个负数相除的结果还是正数，而如果只有一个操作数有符号，那么结果就是负数。如果商超过了 ECMAScript 数值的表示范围， 则返回 Infinity 或 -Infinity ；

```javascript
console.log((Number.MAX_VALUE * 10) / 100); // Infinity
console.log((Number.MAX_VALUE * 10) / -100); // -Infinity
```

#### 如果有一个操作数是 NaN ，则结果是 NaN ；

```javascript
console.log((Number.MAX_VALUE * 10) / NaN); // NaN
console.log(NaN / 0); // NaN
```

#### 如果是 Infinity 被 Infinity 除，则结果是 NaN ；

```javascript
console.log(((Number.MAX_VALUE * 10) / Number.MAX_VALUE) * 100); // Infinity
```

```javascript
console.log(((Number.MAX_VALUE * 10) / Number.MAX_VALUE) * 100); // Infinity
console.log((Number.MAX_VALUE * 10) / (Number.MAX_VALUE * 100)); // NaN

console.log(Number.MAX_VALUE); // 1.7976931348623157e+308
console.log(Number.MAX_VALUE * 10); // Infinity
```

#### 如果是零被零除，则结果是 NaN ；

```javascript
console.log(0 / 0); // NaN
```

#### 如果是非零的有限数被零除，则结果是 Infinity 或 -Infinity ，取决于有符号操作数的符号；

```javascript
console.log(123 / 0); // Infinity
console.log(0 / 123); // 0
```

```javascript
console.log(-123 / 0); // -Infinity
```

#### 如果是 Infinity 被任何非零数值除，则结果是 Infinity 或 -Infinity ，取决于有符号操作数的符号；

```javascript
console.log((Number.MAX_VALUE * 10) / 123); // Infinity
console.log((Number.MAX_VALUE * 10) / 0); // Infinity
console.log(1 / 0); // Infinity
```

#### 如果有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的规则。

```javascript
console.log(1 / []); // Infinity
```

```javascript
console.log(1 / []); // Infinity
console.log(1 / [1, 2, 3, 4]); // NaN
console.log(1 / {}); // NaN
console.log(1 / { sex: "male" }); // NaN
```

#### 如果是 boolean 值, 会转成 0 或者 1, true==>1, false==>0

```javascript
console.log(1 * true); // 1
console.log(1 / true); // 1
console.log(1 * false); // 0
console.log(1 / false); // infinity
```

## 求模

```Javascript
var result = 26 % 5;
```

```javascript
var num = 26 % 5;
console.log(num); // 1
console.log(parseInt(26 / 5)); // 5
console.log(26 / 5); // 5.2
```

与另外两个乘性操作符类似，求模操作符会遵循下列特殊规则来处理特殊的值：

#### 如果操作数都是数值，执行常规的除法计算，返回除得的余数；

#### 如果被除数是无穷大值而除数是有限大的数值，则结果是 NaN ；

```javascript
console.log((Number.MAX_VALUE * 10) % 123); // NaN
```

#### 如果被除数是有限大的数值而除数是零，则结果是 NaN ；

```javascript
console.log(10 % 0); // NaN
```

#### 如果是 Infinity 被 Infinity 除，则结果是 NaN ；

```javascript
console.log((Number.MAX_VALUE * 10) % (Number.MAX_VALUE * 10)); // NaN
```

#### 如果被除数是有限大的数值而除数是无穷大的数值，则结果是被除数；

```javascript
console.log(123 % (Number.MAX_VALUE * 10)); // 123
```

#### 如果被除数是零，则结果是零；

```javascript
console.log(0 % 123); //0
console.log(0 % (Number.MAX_VALUE * 10)); //0
```

#### 如果有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的规则。

#### 0 % 0 是 NaN

```javascript
console.log([] % (Number.MAX_VALUE * 10)); //0
```

```javascript
console.log([] % (Number.MAX_VALUE * 10)); //0
console.log([1, 2, 3] % (Number.MAX_VALUE * 10)); //NaN
console.log({} % (Number.MAX_VALUE * 10)); //NaN
console.log({ sex: "male" } % (Number.MAX_VALUE * 10)); //NaN
```

# 加性操作符

## 加法

加法操作符（+）的用法如下所示：

```javascript
var result = 1 + 2;
```

如果两个操作符都是数值，执行常规的加法计算，然后根据下列规则返回结果：

#### 如果有一个操作数是 NaN ，则结果是 NaN ；

```javascript
console.log(NaN + 1); // NaN
```

#### 如果是 Infinity 加 Infinity ，则结果是 Infinity ；

#### 如果是 -Infinity 加 -Infinity ，则结果是 -Infinity ；

#### 如果是 Infinity 加 -Infinity ，则结果是 NaN ；

```javascript
console.log(Number.MAX_VALUE * 10 + Number.MAX_VALUE * 10); // infinity
console.log(-Infinity + -Infinity); // -Infinity
console.log(-1 + -1); // -2
console.log(-Infinity + Infinity); // NaN
```

#### 如果是+0 加+0，则结果是+0；

#### 如果是-0 加-0，则结果是-0；

#### 如果是+0 加-0，则结果是+0。

```javascript
console.log(+0 + +0); // 0
console.log(-0 + -0); // -0
console.log(-0 + +0); // 0
console.log(+0); // 0
```

不过，如果有一个操作数是字符串，那么就要应用如下规则：

#### 如果两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来；

#### 如果只有一个操作数是字符串，则将另一个操作数转换为字符串，然后再将两个字符串拼接起来。

```javascript
console.log("I love" + " China"); // I love China
console.log("I love" + 123); // I love123
console.log(123 + "I love"); // 123I love

console.log(typeof (123 + "")); // string
```

#### 如果有一个操作数是对象、数值或布尔值，则调用它们的 toString() 方法取得相应的字符串值 然后再应用前面关于字符串的规则。

```javascript
console.log({} + {}); // "[object Object][object Object]"
console.log({}.toString() + {}.toString()); // "[object Object][object Object]"

console.log(typeof {}.toString()); // string
console.log({}.toString()); // "[object Object]"
```

```javascript
console.log("I lvoe" + [] + "China"); // I lvoeChina
console.log("I lvoe" + [1, 2, 3] + "China"); // I lvoe1,2,3China

console.log([].toString()); // ""
console.log([1, 2, 3].toString()); // 1,2,3
```

#### 对于 undefined 和 null ，则分别调用 String() 函数并取得字符串 "undefined" 和 "null" 。

```javascript
console.log("hello" + undefined); // "helloundefined"
console.log("hello" + null); // "hellonull"
console.log("hello" + NaN); // "helloNaN"
console.log(undefined + "hello"); // "undefinedhello"
console.log(null + "hello"); // "nullhello"
console.log(NaN + "hello"); // "NaNhello"
```

```javascript
var result1 = 5 + 5; // 两个数值相加
console.log(result1); // 10
```

```javascript
var result2 = 5 + "5"; // 一个数值和一个字符串相加
console.log(result2); // "55"
```

```javascript
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + num1 + num2;
console.log(message); // "The sum of 5 and 10 is 510"
```

```javascript
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + (num1 + num2);
console.log(message); //"The sum of 5 and 10 is 15"
```

```Javasript
var result1 = 5 + 5;
console.log(result1); // 10
var result2 = 5 + "5";
console.log(result2); // 55
var num1 = 5;
var num2 = 10;
var message = "The sum of 5 and 10 is " + num1 + num2; // The sum of 5 and 10 is 510
var message = "The sum of 5 and 10 is " + (num1 + num2); // The sum of 5 and 10 is 15
var message = "The sum of 5 and 10 is " + 15; // The sum of 5 and 10 is 15
console.log(message); // The sum of 5 and 10 is 15
```

## 减法

```javascript
var result = 2 - 1;
```

#### 如果两个操作符都是数值，则执行常规的算术减法操作并返回结果；

#### 如果有一个操作数是 NaN ，则结果是 NaN ；

```javascript
console.log("hello" - "hello"); // NaN
```

#### 如果是 Infinity 减 Infinity ，则结果是 NaN ；

#### 如果是 -Infinity 减 -Infinity ，则结果是 NaN ；

#### 如果是 Infinity 减 -Infinity ，则结果是 Infinity ；

#### 如果是 -Infinity 减 Infinity ，则结果是 -Infinity ；

```javascript
console.log(Infinity - Infinity); // NaN
console.log(-Infinity - -Infinity); // NaN
console.log(Infinity - Infinity); // NaN
console.log(Infinity - -Infinity); // Infinity
console.log(-Infinity - Infinity); // -Infinity
```

#### 如果是+0 减+0，则结果是+0；

#### 如果是+0 减-0，则结果是+0；

#### 如果是-0 减-0，则结果是+0；

```javascript
// 如果是+0 减+0，则结果是+0；
console.log(+0 - +0); // 0

// 如果是+0 减-0，则结果是0；
console.log(+0 - -0); //0

// 如果是-0 减-0，则结果是+0；
console.log(-0 - -0); //0
```

#### 如果有一个操作数是字符串、布尔值、 null 或 undefined ，则先在后台调用 Number() 函数将其转换为数值，然后再根据前面的规则执行减法计算。如果转换的结果是 NaN ，则减法的结果就是 NaN ；

#### 如果有一个操作数是对象，则调用对象的 valueOf() 方法以取得表示该对象的数值。如果得到的值是 NaN ，则减法的结果就是 NaN 。如果对象没有 valueOf() 方法，则调用其 toString()方法并将得到的字符串转换为数值。

```javascript
console.log(true - false); // 1
console.log(null - false); // 0
console.log(undefined - false); // NaN

console.log(Number(null)); // 0
console.log(Number(undefined)); // NaN
```

```javascript
var result1 = 5 - true; // 4，因为 true 被转换成了 1
var result2 = NaN - 1; // NaN
var result3 = 5 - 3; // 2
var result4 = 5 - ""; // 5，因为"" 被转换成了 0
var result5 = 5 - "2"; // 3，因为"2"被转换成了 2
var result6 = 5 - null; // 5，因为 null 被转换成了 0
```

```javascript
console.log("123" - "456"); //-333
console.log("123mm" - "456nn"); //NaN
```

```javascript
console.log("123" - []); //123
console.log("123" - [1, 2, 3]); //NaN
console.log("123" - {}); //NaN
console.log("123" - { sex: "male" }); //NaN
```

# 关系操作符

小于（<）、大于（>）、小于等于（<=）和大于等于（>=）这几个关系操作符用于对两个值进行比较，这几个操作符都返回一个布尔值

```javascript
var result1 = 5 > 3; //true
var result2 = 5 < 3; //false
console.log(result1);
console.log(result2);
```

```javascript
console.log(3 < 2); //false
console.log(3 > 2); // true
console.log(3 >= 2); // true
console.log(3 <= 2); // false
console.log(2 <= 2); // true
```

当关系操作符的操作数使用了非数值时，也要进行数据转换

1. 如果两个操作数都是数值，则执行数值比较。
1. 如果两个操作数都是字符串，则比较两个字符串对应的字符编码值。

```javascript
console.log("hello" >= "world"); // false
console.log("hello" > "world"); // false
```

1. 如果一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较。

```javascript
console.log(123 > "123"); //false
console.log(123 >= "123"); //true
console.log(123 >= "123hello"); // false
console.log(123 >= []); // true
```

1. 如果一个操作数是对象，则调用这个对象的 valueOf() 方法，用得到的结果按照前面的规则执行比较。如果对象没有 valueOf() 方法，则调用 toString() 方法，并用得到的结果根据前面的规则执行比较。
1. 如果一个操作数是布尔值，则先将其转换为数值，然后再执行比较。

```javascript
console.log(1 > false); // true
console.log(1 > true); // false
```

由于大写字母的字符编码全部小于小写字母的字符编码

```javascript
var result = "Brick" < "alphabet"; //true
console.log(result);
```

```javascript
var result = "Brick".toLowerCase() < "alphabet".toLowerCase(); //false
console.log(result);
```

```javascript
var result = "23" < "3";
console.log(result);
```

```javascript
var result = "23" < 3;
console.log(result);
```

```javascript
var result = "a" < 3;
console.log(result);
```

由于字母 "a" 不能转换成合理的数值，因此就被转换成了 NaN 。
根据规则，任何操作数与 NaN 进行关系比较，结果都是 false 。

```javascript
var result1 = NaN < 3; //false
var result2 = NaN >= 3; //false
console.log(result1);
console.log(result2);
```

```javascript
var result = "Brick" < "alphabet"; // true
var result = "Brick".toLowerCase() < "alphabet".toLowerCase(); // false
var result = "23" < 3; // false
var result = "a" < 3; // false
var result = "a" > 3; // false

console.log(result);
```

# 相等操作符

确定两个变量是否相等是编程中的一个非常重要的操作。在比较字符串、数值和布尔值的相等性时， 问题还比较简单。但在涉及到对象的比较时，问题就变得复杂了。最早的 ECMAScript 中的相等和不等 操作符会在执行比较之前，先将对象转换成相似的类型。后来，有人提出了这种转换到底是否合理的质疑。最后，ECMAScript 的解决方案就是提供两组操作符：
**相等和不相等——先转换再比较，全等和不全等——仅比较而不转换。**

1. 相等和不相等
   ECMAScript 中的相等操作符由两个等于号（ == ）表示，如果两个操作数相等，则返回 true 。
   而不相等操作符由叹号后跟等于号（ != ）表示，如果两个操作数不相等，则返回 true 。
   这两个操作符都会先转换操作数，然后再比较它们的相等性。
   在转换不同的数据类型时，相等和不相等操作符遵循下列基本规则：
1. 如果有一个操作数是布尔值，则在比较相等性之前先将其转换为数值—— false 转换为 0，而 true 转换为 1；

```javascript
console.log(false == 1); // false
console.log(false == 0); // true
console.log(true == 0); // false
console.log(true == 1); // true
```

1. 如果一个操作数是字符串，另一个操作数是数值，在比较相等性之前先将字符串转换为数值；

```javascript
console.log("123" == 123); // true
console.log("123hello" == 123); // false
console.log("[]" == 0); // false
console.log([] == 0); // true
```

1. 如果一个操作数是对象，另一个操作数不是，则调用对象的 valueOf() 方法，用得到的基本类型值按照前面的规则进行比较；这两个操作符在进行比较时则要遵循下列规则。
    1. null 和 undefined 是相等的。
    1. 要比较相等性之前，不能将 null 和 undefined 转换成其他任何值。
    1. 如果有一个操作数是 NaN ，则相等操作符返回 false ，而不相等操作符返回 true 。重要提示： 即使两个操作数都是 NaN ，相等操作符也返回 false ；因为按照规则， NaN 不等于 NaN 。

```javascript
console.log(null == undefined); // true

console.log(NaN == 0); // false
console.log(NaN == "hello"); // false
console.log(NaN == NaN); // false
```

    1. 如果两个操作数都是对象，则比较它们是不是同一个对象。如果两个操作数都指向同一个对象， 则相等操作符返回 true ；否则，返回 false 。

```javascript
console.log([] == []); // false
console.log(new Array() == new Array()); // false

var a = [];
var b = a;
console.log(a == b); // true
```

```javascript
console.log(null == undefined); // true
console.log(true == 1); // true
console.log("NaN" == NaN); // false
console.log(true == 2); // false
console.log(5 == NaN); // false
console.log(undefined == 0); // false
console.log(NaN == NaN); // false
console.log(null == 0); // false
console.log(NaN != 3); // true
console.log(NaN == 3); // false
console.log("5" == 5); // true
console.log(false == 0); // true

console.log(NaN > NaN); // false
console.log(NaN < NaN); // false
```

## 全等和不全等

除了在比较之前不转换操作数之外，全等和不全等操作符与相等和不相等操作符没有什么区别。全等操作符由 3 个等于号（ === ）表示，它只在两个操作数未经转换就相等的情况下返回 true

```javascript
var result1 = "55" == 55; //true，因为转换后相等
var result2 = "55" === 55; //false，因为不同的数据类型不相等
console.log(result1);
console.log(result2);
```

不全等操作符由一个叹号后跟两个等于号（ !== ）表示，它在两个操作数未经转换就不相等的情况下返回 true

```Javascript
var result1 = ("55" != 55); //false，因为转换后相等
var result2 = ("55" !== 55); //true，因为不同的数据类型不相等
console.log(result1);
console.log(result2);
```

```javascript
console.log("123" === 123); // false
console.log("" === []); // false
console.log(0 === []); // false
console.log(null === undefined); // false
```

null == undefined 会返回 true ，因为它们是类似的值；
但 null === undefined 会返回 false ，因为它们是不同类型的值。
由于相等和不相等操作符存在类型转换问题，而为了保持代码中数据类型的完整性，推荐使用全等和不全等操作符

# 条件操作符(三元运算)

## 表达式和语句

```javascript
var age = 17; // 语句
123 > 13; // 表达式
```

有结果的语句, 就叫表达式
`variable = boolean_expression ? true_value : false_value;`
本质上，这行代码的含义就是基于对 boolean_expression 求值的结果，决定给变量 variable 赋什么值。
如果求值结果为 true ，则给变量 variable 赋 true_value 值；如果求值结果为 false ， 则给变量 variable 赋 false_value 值。
`var max = (num1 > num2) ? num1 : num2;`

```javascript
var a = 123 > 333 ? "yes" : "no";
console.log(a); // no
```

```javascript
var a = 3;
var b = 1;
var c = 4;

var max = (a > b ? a : b) > c ? (a > b ? a : b) : c;
console.log(max);
```

比 if 语句更简单

```javascript
var a = 3;
var b = 4;
var c;
if (a > b) {
    c = a;
} else {
    c = b;
}

console.log(c); // 4
```

```javascript
var a = 3;
var b = 4;
var c = 1;
var max;

if (a > b) {
    max = a;
} else {
    max = b;
}

if (max < c) {
    max = c;
}
console.log(max); // 4
```

# 赋值操作符

> 简单的赋值操作符由等于号（ = ）表示，其作用就是把右侧的值赋给左侧的变量

```Javascript
var num = 10;
console.log(num)
```

如果在等于号（ = ）前面再添加乘性操作符、加性操作符或位操作符，就可以完成复合赋值操作。
这种复合赋值操作相当于是对下面常规表达式的简写形式：

```javascript
var num+=10
var num = 10;
num = num + 10;
```

```javascript
var a = "hello";
console.log((a += "world")); // helloworld

// var a = "hello";
// a = a + "world";
```

每个主要算术操作符（以及个别的其他操作符）都有对应的复合赋值操作符。这些操作符如下所示：

`乘/赋值（ *= ）；`

`除/赋值（ /= ）；`

`模/赋值（ %= ）；`

`加/赋值（ += ）；`

`减/赋值（ -= ）；`

<!-- `左移/赋值（ <<= ）；` -->
<!-- `无符号右移/赋值（ >>>= ）。` -->

```javascript
var a = 123;
console.log((a *= 10)); // 1230
var b = 10;
console.log((b /= 10)); // 1
// b/=10   ====> b = b/10

var c = 13;
console.log((c -= 1)); // 12

var d = 24;
console.log((d %= 5)); // 4
```

**设计这些操作符的主要目的就是简化赋值操作。使用它们不会带来任何性能的提升。**(测试时间)

```javascript
// var a = "hello";
// var b = a+="world";
// console.log(b);

var a = "hello";
var b = a + "world";
console.log(b);
```

# 逗号操作符

> 使用逗号操作符可以在一条语句中执行多个操作

```Javascript
var num1=1, num2=2, num3=3;
```

逗号操作符还可以用于赋值。
在用于赋值时，逗号操作符总会返回表达式中的最后一项

```javascript
var num = (5, 1, 4, 8, 0); // num 的值为 0
```

```javascript
var num = (1, 2, 3, 4, 5);
console.log(num); // 5

var num = 1;
num = 2;
num = 3;
num = 4;
num = 5;
console.log(num); // 5
```
