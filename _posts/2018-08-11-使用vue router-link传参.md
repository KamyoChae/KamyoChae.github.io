---
layout: post
title: 使用vue router-link传参
tags: [vue]
---

- 需求：使用vue不刷新页面不使用ajax，改变url地址并显示局部页面
- 实现方式：通过router-link查询字符串方式或path方式实现

# 如何传参 （How to pass the reference）
html：
```html
<div id="app"></div>
```
javascript:
```javascript
        Vue.use(VueRouter);

        var Login = {
            template: `<div>登录界面</div>`,
            created: function () {
               // 查看该组件创建完毕传来的url值
               // console.log(this.$route.query)
            }
        }

        var Register = {
            template: `<div>注册界面</div>`,
            created: function () {
                // 查看该组件创建完毕传来的url值
                // console.log(this.$route.params)
            }
        }
```

```javascript
        var router = new VueRouter({
            // 这里可以直接传 也可以不传
            // 4. 配置路由对象
            routes: [

                { name: "login", path: "/login", component: Login },
                
                // 注意这里的 /:name
                { name: "register", path: "/register/:name", component: Register }

            ] //login 是一个组件对象

        });
```
```javascript
        var App = {
            template: `
                <div>
                    <router-link :to="{name:'login', query:{id:1}}">点我登录</router-link>
                    
                    <router-link :to="{name:'register', params:{name:'abc'}}">点我注册</router-link>
                    <router-view></router-view>
                </div>
            `
        }
        
```
```javascript
        new Vue({
            el: '#app',

            router: router, // 将配置好的路由对象关联到vue实例中
            components: {
                app: App
            },
            template: `<app />`,
            

        })
```
#### 查询字符串方式：在router-link中的to里面写上[query:{id:1}]()
例：

```
<router-link :to="{name:'login', query:{id:1}}">点我登录</router-link>
```
使用查询字符串方式传参，id值会在url中以？id=1的方式添加到末尾


#### path方式：在router-link的to里面写上[params:{name:'abc'}]()
例：

```
      <router-link :to="{name:'register', params:{name:'abc'}}">点我注册</router-link>
                    
```
使用path传参方式，params对象的属性需要在路由配置里面即routes中补上形参，如：

```
  { name: "register", path: "/register/:name", component: Register }
```
这时候params的name才会匹配上对应的link实现url地址的改变

---


# 如何获取传参值 （How to get url pass value）

在对应的模块中，使用this.$route.query或this.$route.params即可获取url实参
- 如果是查询字符串方式，则用query
- 如果是path方式，则用params
例如：

```javascript
        var Login = {
            template: `<div>登录界面</div>`,
            created: function () {
                console.log(this.$route.query)
                // {id:1}
            }
        }

        var Register = {
            template: `<div>注册界面</div>`,
            created: function () {
                console.log(this.$route.params)
                // {name:"abc"}
            }
        }
```


[demo源码](
https://github.com/KamyoChae/Blog/blob/master/vue/articleDemo/09_router-link传参.html)