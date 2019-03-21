---
layout: post
title: js_CommonJs、AMD、CMD模块化开发(3)
tags: [javascript]
---

# 三、CMD
人类的需求是无止境的，有了异步加载我们还不够，还想要个异步按需加载，于是就有了CMD规范

##  CMD 
 首先我们需要下载一个sea.js文件，有了sea.js，通过define定义一个模块 使用require来加载一个模块，就能实现 “就近加载 按需加载”




### 操作方法：
1、在html使用过script元素插入seajs文件 并调用主入口js文件

html:
```javascript
<script src="sea.js"></script>
<script>
    seajs.use("main.js")
<script>
```


2、主入口文件通过define一个模块 该模块练使用require加载一个模块

main.js:
```javascript
define(function(require, exports, module){
    var module = require("module1.js")
    console.log(module) // m1 2m
})

```
3、封装一个模块 通过exports暴露接口给调用者


module1.js:
```javascript
define(function(require, exports, module){

    var arr = [1,2,3,4]
    exports.m1 = "123546789"
    exports.m2 = arr
})
```
[上上篇：CommonJs模块化开发]()

[上一篇：AMD模块化开发]()