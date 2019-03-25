# <%= EJS %>
> 高效的 JavaScript 模板引擎。
>>"E" 代表 "effective"，即【高效】。EJS 是一套简单的模板语言，帮你利用普通的 JavaScript 代码生成 HTML 页面。EJS 没有如何组织内容的教条；也没有再造一套迭代和控制流语法；有的只是普通的 JavaScript 代码而已。

## 特性
+ 快速编译与绘制输出
+ 简洁的模板标签：<% %>
+ 自定义分割符（例如：用 <? ?> 替换 <% %>）
+ 引入模板片段
+ 同时支持服务器端和浏览器 JS 环境
+ JavaScript 中间结果静态缓存
+ 模板静态缓存
+ 兼容 Express 视图系统

## 入门
### node中使用
```
$ npm install ejs
var ejs = require('ejs'),
people = ['geddy', 'neil', 'alex'],
html = ejs.render('<%= people.join(", "); %>', {people: people});
```
### 浏览器支持
```
<script src="ejs.js"></script>
<script>
  var people = ['geddy', 'neil', 'alex'],
      html = ejs.render('<%= people.join(", "); %>', {people: people});
</script>
```

## 文档
### 实例
```
<% if (user) { %>
  <h2><%= user.name %></h2>
<% } %>
```
#### 用法
```
var template = ejs.compile(str, options);
template(data);
// => 输出绘制后的 HTML 字符串

ejs.render(str, data, options);
// => 输出绘制后的 HTML 字符串

ejs.renderFile(filename, data, options, function(err, str){
    // str => 输出绘制后的 HTML 字符串
});
```

## 标签含义
+ <% '脚本' 标签，用于流程控制，无输出。
+ <%_ 删除其前面的空格符
+ <%= 输出数据到模板（输出是转义 HTML 标签）
+ <%- 输出非转义的数据到模板
+ <%# 注释标签，不执行、不输出内容
+ <%% 输出字符串 '<%'
+ %> 一般结束标签
+ -%> 删除紧随其后的换行符
+ _%> 将结束标签后面的空格符删除

## 包含（include）
>>通过 include 指令将相对于模板路径中的模板片段包含进来。(需要提供 'filename' 参数。) 例如，如果存在 "./views/users.ejs" 和 "./views/user/show.ejs" 两个模板文件，你可以通过 <%- include('user/show'); %> 代码包含后者。

>>你可能需要能够输出原始内容的标签 (<%-) 用于 include 指令，避免对输出的 HTML 代码做转义处理。

```
<ul>
  <% users.forEach(function(user){ %>
    <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```

## 自定义分隔符
>>可针对单个模板或全局使用自定义分隔符：
```
var ejs = require('ejs'),
    users = ['geddy', 'neil', 'alex'];

// 单个模板文件
ejs.render('<?= users.join(" | "); ?>', {users: users},
    {delimiter: '?'});
// => 'geddy | neil | alex'

// 全局
ejs.delimiter = '$';
ejs.render('<$= users.join(" | "); $>', {users: users});
// => 'geddy | neil | alex'
```