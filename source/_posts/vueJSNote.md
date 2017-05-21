---
title: vueJSNote
date: 2017-02-19 20:58:17
tags:
      - vueJS
      - props
      - $on
      - $emit
categories: 前端框架
---

#### [see my vueJS demo](http://www.icetower.cn/vue/)
## 使用 Prop 传递数据

组件实例的作用域是孤立的。这意味着不能并且不应该在子组件的模板内直接引用父组件的数据。可以使用 props 把数据传给子组件。
prop 是父组件用来传递数据的一个自定义属性。子组件需要显式地用 props 选项声明 “prop”：
```bash
Vue.component('child', {
  // 声明 props
  props: ['message'],
  // 就像 data 一样，prop 可以用在模板内
  // 同样也可以在 vm 实例中像 “this.message” 这样使用
  template: '<span>{{ message }}</span>'
})
```
然后向它传入一个普通字符串：
```bash
<child message="hello!"></child>
```
输出结果： hello!

## 使用 v-on 绑定自定义事件

每个 Vue 实例都实现了事件接口(Events interface)，即：
使用 $on(eventName) 监听事件
使用 $emit(eventName) 触发事件
Vue的事件系统分离自浏览器的EventTarget API。尽管它们的运行类似，但是$on 和 $emit 不是addEventListener 和 dispatchEvent 的别名。

另外，父组件可以在使用子组件的地方直接用 v-on 来监听子组件触发的事件。
下面是一个例子：
```bash
<div id="counter-event-example">
  <p>{{ total }}</p>
  <button-counter v-on:increment="incrementTotal"></button-counter>
  <button-counter v-on:increment="incrementTotal"></button-counter>
</div>
```
```bash
Vue.component('button-counter', {
  template: '<button v-on:click="increment">{{ counter }}</button>',
  data: function () {
    return {
      counter: 0
    }
  },
  methods: {
    increment: function () {
      this.counter += 1
      this.$emit('increment')
    }
  },
})
new Vue({
  el: '#counter-event-example',
  data: {
    total: 0
  },
  methods: {
    incrementTotal: function () {
      this.total += 1
    }
  }
})
```
## 非父子组件通信

有时候非父子关系的组件也需要通信。在简单的场景下，使用一个空的 Vue 实例作为中央事件总线：
```bash
var bus = new Vue()
```
// 触发组件 A 中的事件
```bash
bus.$emit('id-selected', 1)
```
// 在组件 B 创建的钩子中监听事件
```bash
bus.$on('id-selected', function (id) {
  // ...
})
```
在更多复杂的情况下，你应该考虑使用专门的 状态管理模式.