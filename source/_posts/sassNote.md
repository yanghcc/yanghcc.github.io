---
title: sassNote
date: 2017-02-20 10:19:07
tags:
      - sass
      - compass
      - scss
categories: css
---

## Sass用法指南
Sass是一种基于ruby开发的"CSS预处理器"，可以让CSS的开发变得简单和可维护，语法和less很相近。搭配Compass，sass将会更强大。

## Compass用法指南
### 一、Compass是什么？
简单说，Compass是Sass的工具库（toolkit）。
Sass本身只是一个编译器，Compass在它的基础上，封装了一系列有用的模块和模板，补充Sass的功能。它们之间的关系，有点像Javascript和jQuery、Ruby和Rails、python和Django的关系。

### 二、安装
Compass是用Ruby语言开发的，所以安装它之前，必须安装Ruby。[传送门](https://www.ruby-lang.org/zh_tw/documentation/installation/)
假定你的机器（Linux或OS X）已经安装好Ruby，那么在命令行模式下键入：
```bash
$　　sudo gem install compass
```
如果你用的是Windows系统，那么要省略前面的sudo。
正常情况下，Compass（连同Sass）就安装好了。

### 三、项目初始化
接下来，要创建一个你的Compass项目，假定它的名字叫做myproject，那么在命令行键入：
```bash
$　　compass create myproject
```
当前目录中就会生成一个myproject子目录。
进入该目录：
```bash
$　　cd myproject
```
你会看到，里面有一个config.rb文件，这是你的项目的配置文件。还有两个子目录sass和stylesheets，前者存放Sass源文件，后者存放编译后的css文件。

接下来，就可以动手写代码了。

### 四、Compass编译相关知识:

//scss编译命令
```bash
$  compass compile
```
//scss监听命令，文件改变自动编译
```bash
$  compass watch
```
//默认状态下，编译出来的css文件带有大量的注释。但是，生产环境需要压缩后的css文件，这时要使用--output-style参数
```bash
$  compass compile --output-style compressed
```
//Compass只编译发生变动的文件，如果你要重新编译未变动的文件，需要使用—force参数
```bash
$  compass compile --force
```
//expanded模式表示编译后保留原格式，其他值还包括:nested、:compact和:compressed。进入生产阶段后，就要改为:compressed模式
```bash
$  compass compile output_style = :expanded
```
常用的五个功能模块。编译之后可以自动完善对应的css样式代码
```bash
@import "compass/reset";//加载reset模块,重置样式
@import "compass/css3";//处理兼容性问题
@import "compass/layout";//该模块提供布局功能 eg.  footer
@import "compass/typography";//该模块提供版式功能
@import "compass/utilities";//该模块提供某些不属于其他模块的功能,eg.fix & tab
```
eg.使用CSS3模块，通过@include 引入。编译之后，自动补充浏览器兼容写法。
```bash
$color:#222;//使用$定义变量
.first{
    @include border-radius(5px);
    @include opacity(.5);
    @include inline-block;

    @include clearfix;//清楚浮动
    @include table-scaffolding;//表格

    …
    color:$color;//引用变量
    .second{
        @include stretch;//指定子元素占满父元素的空间
    }
    #footer {
　　 @include sticky-footer(54px);//指定页面的footer部分总是出现在浏览器最底端
　}
}
```
