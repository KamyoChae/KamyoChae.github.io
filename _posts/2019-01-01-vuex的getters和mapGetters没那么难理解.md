---
layout: post
title: vuex的getters和mapGetters没那么难理解
tags: [vue]
---

其实这个getters和mapGetters没必要看得太复杂，在初学vue的时候，看到网上的一些博客，写得云里来雾里去的，一言难尽。今晚看了下[vuex官网](https://vuex.vuejs.org/zh/guide/getters.html)的介绍，有了新的体会，这里写一下理解。

getters相当于我们组件里面的computed，当getters里面依赖的值变化了它就触发一下。

getters在vuex里面是这样写的：

```javascript
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```
它的作用也是一个缓存，todos里面的数据变了它就触发一次doneTodos函数。

以前没搞明白这个，总喜欢在actions里面commit调用mutation里面的函数，而mutation里面又做了大量的数据处理，处理完毕又返回给state，再通过在组件内```this.$store.state.value```调用状态值，进一步削弱了代码质量。

getters完全可以理解成computed，但getters里面一定得有个state形参。

# 
下面说说mapGetters

理解了mapState，再来理解mapGetters就简单多了。

我们可以在组件中通过下面这种写法获取state的值：

```javascript
computed : {
    ...mapState(["todos"])
}
```
那么也就意味着我们可以在组件中通过下面这种写法获取getters的值：
```javascript
computed : {
    ...mapGetters([
      'doneTodos', 
    ])
}
```
mapState中的todos相当于this.$store.state.todos

mapGetters中的doneTodos相当于this.$store.getters.doneTodos

然后就是在组件里面this.todos 、this.doneTodos....

不过别忘了mapState还有一种写法（[上一篇有介绍](https://github.com/KamyoChae/Blog-on-github/issues/59)）：
```javascript
computed : {
    ...mapState({
    storeName : state => state.name
    storeValue : state => state.value
    storeAge : state => state.age
    }),
    count(){
        ...
    },
}
```
mapGetters也是这样写的吗？不是。在mapGetters里面可以这样写：
```javascript
computed : {
    ...mapState({
        storeTodos: state => state.todos 
    }),
    ...mapGetters({
        doneTodos : "doneTodos" 
    }),
    count(){
        ...
    },
}
```
很明显，不用写成函数的样子，而是直接写成键值对的形式。

看上去很难，但用起来就这么简单...嗯



