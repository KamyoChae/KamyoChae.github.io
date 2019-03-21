---
layout: post
title: js_CommonJs、AMD、CMD模块化开发(2)
tags: [javascript]
---


# 二、AMD
若浏览器采用commonjs同步加载js文件，倘若文件过多，则会导致页面瘫痪
为了解决异步加载 让浏览器有足够的时间去加载文件，出现了AMD规范

## AMD规范则是异步加载模块 
允许指定回调函数。指定好了就异步加载，加载完成后即可调用函数

AMD的得意之作就是require.js

##  AMD核心思想：通过define定义模块通过require加载模块 模块前置 提前加载

示例：

 index.js:

```javascript
require(["main1","main2"],function(m1,m2){
    // ["main1","main2"] 变量1 数组里面写上要加载的模块
    // function(m1,m2) 变量2 函数里面的两个形参就是要加载的模块 当变量1加载完毕之后 函数才会执行

})
```

 main1:
```javascript
define(
    function(){
        ...
    }
)

//main2
define(function(){
        function add(a){
            a += a;
        }
    }
)

```

------------


# 如何使用require.js
1、去官网下载
2、将require.js文件引入html页面
3、设置主入口文件main.js -> data-main="main.js" 到script标签
    `<script src="require.js" data-main="main.js"></script>`
4、到main.js文件里写入


 // main.js:
```javascript
require.config({
    // 配置路径
    baseUrl:"../tool/"
    paths:{
        "jquery":"jquery路径"
    }
})
require(["jquery","math"],function($,math){ 
    // 数组里面的东西尽量不要写上路径名字
    // 路径名可以在require.config里面统一定义

    math.add(2) // 通过形参名调用对应文件的函数
})

```
*缺点： 无法按需加载*

[上一篇：CommonJs]() 

[下一篇：CMD]()
