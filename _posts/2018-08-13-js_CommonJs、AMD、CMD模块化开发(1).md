---
layout: post
title: js_CommonJs、AMD、CMD模块化开发(1)
tags: [javascript]
---


## **CommonJs、AMD、CMD的比较**
首先我们来了解一下模块化


（原来的笔记太长了，分成三篇文章方便阅读。[原笔记链接](https://github.com/KamyoChae/Blog/blob/master/js/es5/%E6%A8%A1%E5%9D%97%E5%8C%96%E5%BC%80%E5%8F%91%E4%B9%8BCommonJs%E3%80%81AMD%E3%80%81CMD.md)）

------------

我们经常这样子写代码

1. 函数 （函数模块化）
```javascript
funcion add(a,b){
    return a+b
}
console.log(add(45+45))`
```
*缺点：只能在某个作用域内使用*

1. 对象（对象模块化）
```javascript
var ppt = {
    len:3,
    init:function(){},
    createDom:function(){}
}
```
*优点：简单快速
弊端：外部可影响内部属性*

1. 匿名函数 
```javascript
var obj = (function(){
    var len = 5;
    function add(a,b){
        return a+b'
    }
    return {
        add:add;
    }
}())
console.log(obj.add(1,2))
```
*优点：变量私有化
缺点：要return*

1.  依赖
```javascript
(function (a,b){
    b(a)
})(window, function(window){
    window.jquery = jquery;
    function jquery (){}
})
```
*缺点：只能在该模块中不断添加方法*

1. 模块化开发
```javascript
(function (m){
m.add = function(){
}
})(window.module || {})
```
*优点：能对已有基础添加方法*



### 可见，如果多个人共同开发某个项目，大家都在用自己喜欢的写法，那么整个项目的代码是非常糟糕的。为了实现js代码战国时代的大一统，彻底终结时代动乱，纵横家“苏秦”出现了，也就是我们现在说的“模块化开发规范”




------------




## 模块化出现的时代背景
1. 最初js并没有模块化机制
2. 各种野生js到处飞 得不到妥善管理
3. 后来前端圈开始制定规范 出现了commonjs 
4. node就是基于commonjs规范的产物（commonjs同步加载 适用于服务器端）
5. 由于commonjs的同步加载更适用于服务器端 
6. 所以迫切需要客户端的规范出台
7. 旋即出现了很多耳熟能详的前端规范 如AMD

------------



# 一、CommonJs：
##### 特点： 一个萝卜一个坑，一个文件一个模块
一个js文件就是一个模块，内部变量属于该模块， 不会对外部暴露， 也就是不会污染全局变量

该规范最初用在node，前端的webpack对CommonJs原生支持

##### 核心思想 
通过require方法同步加载所需要依赖的其他模块
然后通过 exports或者module.exports来导出暴露的接口

如:

###### // index.js
```javascript

var module = require("module.js")

module.add(5) 

```
###### // module.js
```javascript

module.exports = {
    aad:function (n){
       return  n += 5
    }
}
```
如果你觉得只要照葫芦画瓢，把这段代码复制粘贴到项目里面，那就大错特错了哦

###### 浏览器不兼容Commonjs ，因为缺少 module exports require global环境变量。
###### 它需要工具转换才能成功运行

##### commonJs缺点：同步加载，适用服务器端，服务器读取加载时间快，但不适合移动端


[下一篇：AMD模块化开发]() 

[下下篇：CMD模块化开发]()
