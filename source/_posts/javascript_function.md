---
title: javascript函数
date: 2017-02-21 14:16:02
tags:
     - javascript
     - function
categories: javaScript
---
### 函数声明（静态函数）
函数声明有个特征就是函数可以函数声明提前
```bash
hello();
function hello(){
console.log('hello js');
}
```
函数表达式（Function expressions）
```bash
var hello2 = function(){
 console.log('hello2 js');
}
hello2();
```
这种方式命名，没有函数声明提前，这个方式也是自己比较喜欢用的方式。

### 匿名函数（ anonymous）
```bash
(function(){
    console.log('message');
})()
```
也可以直接传入变量，jQuery源码用的比较的多，用匿名函数的好处就是可以减少命名的冲突，省的为了只执行一次的函数你还要去命名
```bash
(function(e){
    console.log(e);
})(2)
```
自动执行的其他的写法
```bash
var auto = (function(){
     console.log('auto message');
})()

var auto = (function(){
    console.log('auto message2');
}())
```

### 回调函数（callback）
就是把函数当做变量，这个算是js中比较特别的地方，nodejs的异步回调的大体就是那样
```bash
function person(callback,name,age){
    callback(name,age);
}
function output(name,age){
    console.log(name+':'+age);
}
new person(output,'zs',18);
```

### 递归函数
关于递归，这个平时很少应用。简单的说就是自己调用自己：
```bash
function add(n){
    if(n<=1){
        return 1;
    }else{
        return n+add(n-1)
    }
}
// var i= add(4);
console.log(add(4));
```

### 构造函数
```bash
* 构造函数首字母大写
* this用法，指向本身，这个比较复杂，以后总结好了，弄明白了再细说
* 闭包问题也是比较头痛的问题，留在以后。会造成内存消耗
构造函数的三部曲：

* 构造方法
* 定义属性
* 原型法定义函数，这样比较的节省内存
* 函数的继承，call，apply（用在传递数组）

函数的继承：
function Person(name,age){
    this.name=name;
    this.age=age;
}

Person.prototype.out=function(){
    var self=this;
    console.log(this.name+':'+this.age);
}

function Student(name,age,id){
    // Person.call(this,name,age);
    Person.apply(this,[name,age]);//或是用apply都行
    this.id=id;
}
Student.prototype.output=function(){
    var self=this;
    console.log(this.name+':'+this.age+';'+this.id);
}

new Person('lh',18).out();
new Student('KK',18,'XUESHENG').output();
```

### 函数的重载：
主要是通过argument.length分别调用的，没有怎么用过
```bash
function f(x){}
function f(x,y){}
function f(x,y,z){}
```

### 总结最优的命名函数方法：
用构造方法生成成员变量，用原型法生成成员方法，减少内存的消耗
```bash
function Person(name,age){
    this.name=name;
    this.age=age;
    this.say();
    // 这样也行（构造方法分配成员方法），比较喜欢原型法构造函数
    this.say=function(){
        console.log(name+age);
    }
}
Person.prototype.say=function(){
    console.log(name+age);
}
```

### javascript函数封装的方式
1、JS封装就是尽量把使用的方式简单化，内部逻辑和使用解耦。通俗的说就是使用的时候只需要知道参数和返回值，其他条件尽量不要使用人员进行设置。
2、JS封装的方法有函数方式、对象的方式、闭包的方式。

#### 举例
1）函数方式
```bash
function kk(a,b){
   内部对a，b怎么处理就不需要关心了
}
```
2）对象方式
```bash
function kk(a,b){
   this.x = a;
   this.y = b;
}
var k = new kk(1,2);//通过面向对象的方式
alert(k.x);
```
3）闭包方式
```bash
function kk(a,b){
   var k = 1;
   return function tt(){
      k++;
   }
}
var u = kk(1,2);
u();//闭包实现累加
u();//闭包实现累加
```
//简单理解如下：
//封装：将字段，属性，方法等封装成类
//例如：将人封装成一个类，有name,age等字段，有eat方法
```bash
function Person(name, age){
    this._name = name;
    this._age = age;
    this.getAge = function(){
        return this.age;
    };
    this.setAge = function(value){
        this.age = value;
    };
    this.getName = function(){
        return this.name;
    };
    this.eat=function()
    {
        alert(this._name+" Eat!");
    };
}
```
//使用这个类：
```bash
var p1 = new Person("张三", 12);
p1.eat();
```