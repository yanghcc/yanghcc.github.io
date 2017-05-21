---
title: lessNote
date: 2017-02-20 10:05:28
tags:
     - less
     - css
categories: css
---

### 1.less使用@来声明变量。
```bash
@bgc:#cccc;
```
### 2.混合。less可以直接引用选择器，继承其所有样式；less选择器可以传参，默认参数值即是默认属性值。调用时，传参就可以改值。
```bash
#selector(@width:20px){
    width:@width;
}
```
### 3.匹配模式。根据参数选值，调用对应匹配的样式。
```bash
#pos(r){
    posiont:relative;
}
#pos(a){
    posiont:absolute;
}
#pos(f){
    posiont:fixed;
}
```
### 4.数值运算。（包括颜色值，长度值）
eg.
```bash
@fontSize:14px;
 .selector{
    font-size:@fontSize - 2;//12px
}
```
### 5.嵌套。&符号表示其父级。
```bash
ul{
    li{...}
    a{...}
    &:active{...}
}
```
### 6.避免编译，如下100px；不会经过编译。
```bash
 .selector{
    width:~’100px’;
}
```
### 7.变量插值。
```bash
// 定义变量
@mySelector:banner;
```
```bash
// 用法
.@{mySelector}{
    font-weight: bold;
    line-height:40px;
    margin:0auto;
 }
```
### 8.!important,可以直接加在变量后，提升改属性的优先级。
### 9.Scope （作用域）
Less 中的作用域与编程语言中的作用域概念非常相似。首先会在局部查找变量和混合，如果没找到，编译器就会在父作用域中查找，依次类推。
```bash
@var: red;
#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```
### 10.Importing （导入）
导入工作与你预期的一样。你可以导入一个 .less 文件，然后这个文件中的所有变量都可以使用了。对于 .less 文件而言，其扩展名是可选的。
```bash
@import "library"; // library.less
@import "typo.css";
```
### 11.Comments （注释）

可以使用块注释和行注释:
```bash
/* One hell of a block
style comment! */
@var: red;
```
```bash
// Get in line!
@var: white;
```