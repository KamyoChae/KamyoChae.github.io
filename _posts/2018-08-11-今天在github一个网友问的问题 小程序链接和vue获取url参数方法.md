---
layout: post
title: 今天在github一个网友问的问题 小程序链接和vue获取url参数方法
tags: [vue]
---

My opinion on these two issues is this:

针对这两个问题，我的看法是这样的：

---
## 1."shared to the micro-messenger, visit the web page no data, how to solve."
WeChat will intercept the part of the "#" in the shared link, causing the shared source parameter to be truncated, and the page will be loaded.

###  **for example：**
> https://demo.xxx.com/dzp/?from=singlemessage#/dzp/project?friendId=151613270061

In this link, WeChat will cut off "/dzp/project?friendId=151613270061", causing the page to not load.

### **Solution:**
Change the url to:
> http://demo.xxx.com/dzp/?friendId=151613270061&from=singlemessage#/dzp/project


## 
 
微信会将分享出去的链接中”#”号后面部分截取掉了，导致后面带的分享来源参数被截掉了，页面呈现出一直在加载的状态。

### **例如：**
> https://demo.xxx.com/dzp/?from=singlemessage#/dzp/project?friendId=151613270061

在这个链接里面，微信会把”/dzp/project?friendId=151613270061”截掉，导致页面加载不出来

### **解决办法：**
将url改成：
> http://demo.xxx.com/dzp/?friendId=151613270061&from=singlemessage#/dzp/project
即可



---


## 2.“how to call vue-router to get the parameters of URL address bar by introducing Vue with script tag”


By router-link method ```<router-link :to="{name:'login', query:{id:1}}">login page</router-link>``` 

or path mode ```<router-link :to="{name:'register', params:{name:'abc'}}">register page</router-link>``` can put parameters after the url.


If you want to get the value in the url, you can get it by "this.$route.query" or "this.$route.params"

### **E.g:**

```javascript
 var Login = {
    template: `<div>login page</div>`,
    created: function () {
        console.log(this.$route.query)
        // {id:1}
    }
}

var Register = {
    template: `<div>register page</div>`,
    created: function () {
        console.log(this.$route.params)
        // {name:"abc"}
    }
}
```


## 


通过 “router-link”查询字符串方式 
```
<router-link :to="{name:'login', query:{id:1}}">login page</router-link>
```
或path方式
```
<router-link :to="{name:'register', params:{name:'abc'}}">register page</router-link>
```
可以将参数放到url后面。


如果想获取url里面的值，可以通过 ```this.$route.query```
 或者 ```this.$route.params```
获取

### **例如：**


```javascript
var Login = {
            template: `<div>login page</div>`,
            created: function () {
                console.log(this.$route.query)
                // {id:1}
            }
        }

        var Register = {
            template: `<div>register page</div>`,
            created: function () {
                console.log(this.$route.params)
                // {name:"abc"}
            }
        }
```


# **[Related Issues](https://github.com/KamyoChae/Blog/issues/10)**