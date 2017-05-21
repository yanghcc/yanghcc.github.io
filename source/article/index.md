---
title: article
date: 2017-02-20 11:40:27
categories: others
---
### 如果你总是这样轻言放弃的话，无论过多久都只会原地踏步。

web开发大背景：
传统方式>>{处理服务器数据 & 用户输入数据}>>动态反应到网页，这个过程变得越来越复杂，代码量越来越大，后期维护变得越来越难。

### 初识react：
1，react不是一个完整的MVC，MVVM框架，它重点关注view层
2，react跟web components不冲突
3，react的特点是’轻’
4，组件化开发思路，可复用性强

### react应用场景：
1，复杂场景下的高性能
2，重用组件库，组件组合
3，简化代码量，降低后期维护成本

### 前置知识：
1. Js , css 基础
2. Sass ,compass
3. yeoman , grunt , webpack
4. commonJS , NodeJS
5. Git , github

JSX是facebook为react开发的一个语法糖(需要解析成原生JS代码)
例如：coffeeScript , TypeScript

优秀程序员：
无论项目多难多复杂，什么姿势都得上
学会借助外力学习，通过多种路径学习前沿知识
坚持不懈

### react事件

粘贴板事件，包括
- onCopy
- onCut
- onPaste

只有onPaste事件触发时才能访问clipboardData事件对象，通过getData()方法（该方法至少需要一个参数，eg.’Text’,'text/plain’,’url’…），获取当前粘贴板的数据。
