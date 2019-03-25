# 什么是语句?

> 一行代码就是一个语句, 分号结束

## 什么是流程控制语句?

> 可以改变代码运行顺序的语句
> 包括`顺序语句`,`分支语句`,`循环语句`
> 三种语句结合, 可以解决所有问题, 不需要新的类型的语句

### 顺序语句

> 可以从上到下, 从左往右顺序执行的语句

### 分支语句

> 根据条件不同, 选择一部分语句执行
> 第一步, 先判断是否符合条件, 第二步, 做选择

#### if 语句

`if (condition) statement1 else statement2`

自动类型转换

```javascript
if ("hello") {
    console.log(1);
} else {
    console.log(2);
}

console.log(Boolean("hello")); // true
```

```javascript
if ("") {
    console.log(1);
} else {
    console.log(2); // 走这个
}
```

如果分支语句中, 只有一行, 可以省略大括号(花括号), 但是不推荐

```javascript
if ("") console.log(1);
else console.log(2); // 走这个
```

多行一定要加花括号

```javascript
if ("") {
    console.log(1);
    console.log(12);
} else {
    console.log(2); // 走这个
    console.log(23); // 走这个
}
```

更加复杂的
`if (condition) statement1 else if (condition2) statement2 else statement3`

```javascript
var bus46 = true;
var bus47 = true;

if (bus46) {
    console.log("搭乘46路公交车上课"); // 走这个
} else if (bus47) {
    console.log("搭乘47路公交车上课");
} else {
    console.log("没招儿了, 继续等吧, 或者11路");
}
```

```javascript
var bus46 = false;
var bus47 = true;

if (bus46) {
    console.log("搭乘46路公交车上课");
} else if (bus47) {
    console.log("搭乘47路公交车上课"); // 走这个
} else {
    console.log("没招儿了, 继续等吧, 或者11路");
}
```

```javascript
var bus46 = false;
var bus47 = false;

if (bus46) {
    console.log("搭乘46路公交车上课");
} else if (bus47) {
    console.log("搭乘47路公交车上课");
} else {
    console.log("没招儿了, 继续等吧, 或者11路"); // 走这个
}
```

**`else if` 和 `elseif`不同, `elseif`会报错** 

```javascript
var score = 90;

if (score >= 90) {
    console.log("都是九年制义务教育, 你为何如此优秀?"); // 跑这个
} else if (score >= 80) {
    console.log("哎呦, 还不错哦");
} else if (score >= 70) {
    console.log("继续加油, 我看好你呦!");
} else if (score >= 60) {
    console.log("骚年, 需要加把劲了!");
} else {
    console.log("我已经无言以对了...");
}
```

```javascript
var score = 81;

if (score >= 90) {
    console.log("都是九年制义务教育, 你为何如此优秀?");
} else if (score >= 80) {
    console.log("哎呦, 还不错哦"); // run this statement
} else if (score >= 70) {
    console.log("继续加油, 我看好你呦!");
} else if (score >= 60) {
    console.log("骚年, 需要加把劲了!");
} else {
    console.log("我已经无言以对了...");
}
```

```javascript
var score = 55;

if (score >= 90) {
    console.log("都是九年制义务教育, 你为何如此优秀?");
} else if (score >= 80) {
    console.log("哎呦, 还不错哦");
} else if (score >= 70) {
    console.log("继续加油, 我看好你呦!");
} else if (score >= 60) {
    console.log("骚年, 需要加把劲了!");
} else {
    console.log("我已经无言以对了..."); // run this statement
}
```

if 语句, 越严格的条件, 越放在前面

```javascript
var score = 100;

if (score >= 60) {
    console.log("无言以对");
} else if (score >= 70) {
    console.log("加把劲");
} else if (score >= 80) {
    console.log("看好你");
} else if (score >= 90) {
    console.log("太棒了");
}

// 都是无言以对
```

## switch

> 条件语句的一种

```
switch(expression){
    case value:
        statement
        break;
    case value:
        statement
        break;
        ...
    default:
        statement
}
```

改写原来的 if else 例子

```javascript
var score = 51;

switch (parseInt(score / 10)) {
    case 8:
        console.log("哎呦, 还不错哦");
        break;
    case 7:
        console.log("继续加油, 我看好你呦!");
        break;
    case 9:
        console.log("都是九年制义务教育, 你为何如此优秀?");
        break;
    case 6:
        console.log("骚年, 需要加把劲了!");
        break;

    default:
        console.log("我已经无言以对了...");
}
```

```javascript
var score = 91;

switch (parseInt(score / 10)) {
    case 8:
        console.log("哎呦, 还不错哦");
    case 7:
        console.log("继续加油, 我看好你呦!");
    case 9:
        console.log("都是九年制义务教育, 你为何如此优秀?");
    case 6:
        console.log("骚年, 需要加把劲了!");
    default:
        console.log("我已经无言以对了...");
}
```

也可以使用范围

```javascript
var score = 71;

switch (true) {
    case score >= 80 && score < 90:
        console.log("哎呦, 还不错哦");
        break;
    case score >= 70 && score < 80:
        console.log("继续加油, 我看好你呦!");
        break;
    case score >= 90 && score < 100:
        console.log("都是九年制义务教育, 你为何如此优秀?");
        break;
    case score >= 60 && score < 70:
        console.log("骚年, 需要加把劲了!");
        break;
    default:
        console.log("我已经无言以对了...");
}
```

## switch 和 if else 的区别何在?

1. switch 不用考虑顺序顺序
1. 性能问题比 if else 好一点

整合结果

```javascript
var score = 88;

switch (parseInt(score / 10)) {
    case 8:
    case 7:
    case 9:
    case 6:
        console.log("很好!");
        break;
    default:
        console.log("我已经无言以对了...");
}
```

```javascript
var a = "helloworld";

switch (a) {
    case "hello" + "world":
        console.log("hello world");
        break;
    case "good" + "bye":
        console.log("good bye");
        break;
    default:
        console.log("nothing...");
}
```

```javascript
var a = 123;
// 使用 === 来比较
switch (a) {
    case "12" + "3":
        console.log("hello world");
        break;
    case "good" + "bye":
        console.log("good bye");
        break;
    default:
        console.log("nothing...");
}
```

break, 一般用在 switch 和循环中, 表示终断
在顺序语句和函数中, 一般使用 return

### 循环语句

> 根据条件, 重复执行某一段代码

#### do-while
> 后测试循环语句
```
do{
    statement
}while(expression)
```
```javascript
var i = 0;
do {
    i += 2;
    console.log(i); // 2,4,6,8,10
} while (i < 10);
```


#### while
> 前测试循环语句

```
while(expression) statement
```
```javascript
var i = 0;
while (i < 10) {
    console.log(i); // 0,2,4,6,8
    i += 2;
}
```
#### for
> 前测试循环语句
```
for(initialization; expression; post-loop-expression) statement
```
```javascript
var count = 10;
for (var i = 0; i < count; i++) {
    console.log(i); // 0,1,2,3,4,5,6,7,8,9
}
```

break 终断
```javascript
var count = 10;
for (var i = 0; i < count; i++) {
    if (i == 5) {
        break;
    }
    console.log(i); // 0,1,2,3,4
}
```
continue 继续,跳过本次循环
```javascript
var count = 10;
for (var i = 0; i < count; i++) {
    if (i == 5) {
        continue;
    }
    console.log(i); // 0,1,2,3,4,6,7,8,9
}
```
无限循环
```javascript
var count = 10;
for (;;) {
    console.log(count);
}
```
```javascript
var count = 10;
for (var i = 0; ; i++) {
    console.log(i);
}
```
```javascript
// var count = 10;
// var i = 0;
// while (i < count) {
//     i++;
//     console.log(i);
// }

var count = 10;
var i = 0;
for (; i < count; ) {
    i++;
    console.log(i);
}
```
for和if同时使用
```javascript
var student = "佳佳同学";
var push_up_sum = 40;

for (var push_up_num = 1; push_up_num <= push_up_sum; push_up_num++) {
    console.log(student + "已经做了 " + push_up_num + " 个俯卧撑啦");
    if (push_up_num == push_up_sum) {
        console.log(student + "已经做完了, 目前感觉良好!");
    }
}
```
```javascript
var student = "佳佳同学";
var push_up_sum = 1000;

for (var push_up_num = 1; push_up_num <= push_up_sum; push_up_num++) {
    console.log(student + "已经做了 " + push_up_num + " 个俯卧撑啦");

    if (push_up_num == 50) {
        console.log(student + "有点发虚...");
    }
    if (push_up_num == 100) {
        console.log(student + "表示'我还可以...'");
    }
    if (push_up_num == 200) {
        console.log(student + "居然有了快乐的感觉");
    }
    if (push_up_num == 300) {
        console.log(student + "渐入佳境...");
    }
    if (push_up_num == 500) {
        console.log(student + "已经停不下来了了!");
    }

    if (push_up_num == push_up_sum) {
        console.log(
            student + "表示:'我不是针对谁, 说道俯卧撑, 在座的各位, 都是垃圾'"
        );
    }
}
```