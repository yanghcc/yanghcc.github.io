---
title: 浅谈对MVC，MVVM的理解
tags:
        - mvc
        - mvvm
categories:    前端框架
---

View 传送指令到 Controller

Controller 完成业务逻辑后，要求 Model 改变状态

Model 将新的数据发送到 View，用户得到反馈
所有通信都是单向的。

Angular它采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel，反之亦然。

组成部分Model、View、ViewModel

View：UI界面

ViewModel：它是View的抽象，负责View与Model之间信息转换，将View的Command传送到Model；

Model：数据访问层


### 名词解析
MVC（模型-视图-控制器）
Model(模型)主要与业务数据有关。
View(视图)是关于构件和维护一个DOM元素。应用程序数据的可视化表示。
Controller(控制器）用户更新视图，controller更新model

