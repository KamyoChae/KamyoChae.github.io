
---
layout: post
title: vuex的mapState有三种写法，该怎么用？
tags: vue
---

在组件调用vuex中的 值，我们一般会这样写：const value = this.$store.state.value

当我们在组件中调用几十个vuex中的值时，这样的写法显得有些重复繁琐。这时候mapstate就能发挥巨大作用了。

#### mapstate第一种用法：

我们可以在组件内的计算属性中写成下面这个样子：
```javascript
computed : mapState (["name", "value", "age"])
```
这种写法适合组件内computed没有计算属性的情况下。原因是如果组件内还有其他计算属性，这样写了，别的计算属性往哪塞？另外一个值得注意的是，如果data数据里面有属性和mapState里面的属性相同的话，组件会优先显示data里面的属性值。

因此，第一种写法仅适用data无重名，无计算属性的组件


#### mapstate第二种用法：
```javascript
computed : mapState ({
    storeName : state => state.name
    storeValue : state => state.value
    storeAge : state => state.age
})
```
第二种写法是第一种写法的升级版，这种写法解决的是data重名属性的问题，这里解决的方式是分别给每个state值重新起名。但有一个缺点，这种写法也是适合组件无计算属性的情况下使用。

因此，第二种写法适合无计算属性的组件使用

#### mapstate第三种用法：
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
当我们既想使用mapState，又不想跟data重名，还想给别的计算属性挪地方的话，可以试试第三种写法。

这种写法是第二种写法的升级版，将mapState放到computed计算属性里面，用扩展运算符对mapState进行展开。

这种写法能完美解决上面两种方法带来的不便，data重名不怕、computed也留了空间。

总结：根据不同的组件使用不同的写法能大大提高编程效率，在写代码的过程衡量一下就好了，不必太过纠结哪种写法好与坏