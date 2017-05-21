---
title: javascript事件
date: 2017-02-20 16:40:34
tags:
      - javaScript
      - event
categories: javaScript
---

## 事件自定义

使用自定义事件有助于解耦相关对象,保持功能的隔绝,在很多情况下,触发事件的代码和监听事件的代码是完全分离的.
事件是与DOM交互的最常见的方式,但它也可以用于非DOM代码中--通过实现自定义事件.实现自定义事件的原理是创建一个管理事件的对象.如下代码是事件的定义:
```bash
function EventTarget(){
//存储事件处理程序,由n个键值对组成,键表示事件名,值是一个由事件处理程序组成的数组
this.handlers = {};
}
EventTarget.prototype = {
constructor:EventTarget,
//添加事件
addHandler:function(type,handler){
    if(typeof this.handlers[type] == "undefined"){
        this.handlers[type] = [];
    }
    this.handlers[type].push(handler);
},
//触发事件
fire:function(event){
    if(!event.target){
        event.target = this;
    }
    if(this.handlers[event.type] instanceof Array){
            var handlers = this.handlers[event.type];
            for(var i=0,len=handlers.length;i < len;i++){
                //将event传递给事件处理程序,event.target代表对象本身,
                event.type代表事件名,你可以根据情况为添加event属性
                handlers[i](event);
            }
    }
},
//移除事件
removeHandler:function(type,handler){

    if(this.handlers[type] instanceof Array){

        var handlers=this.handlers[type];

        for(var i=0,len=handlers.length;i < len; i++){
            if(handlers[i] == handler){
                break;
            }
        }

        handlers.splice(i,1);
    }
}
};
首先是定义了一个名为EventTarget的构造函数,为其定义的属性handlers用于存储事件处理程序,
然后有三个操作方法添加到EventTarget的原型中,分别是addHandler fire remocveHander.

addHander是向handlers中添加事件处理程序
fire是触发handlers中的事件处理程序
removeHandler是向handlers中移除事件处理程序

注:事件处理程序通俗的讲就是事件被触发时需要执行的方法.
```
## 事件调用
```bash
var eventObj=new EventTarget(); //实例化一个EventTarget类型

var handler=function(){
    alert('event');
};  //事件处理程序

eventObj.addHandler('alert',handler); //为eventObj对象添加一个事件处理程序`handler`

event.fire({type:'alert'});  //触发eventObj对象中的事件处理程序`handler`

event.removeHandler('alert',handler);  //删除eventObj对象中的事件处理程序`handler`
```
## 事件继承
```bash
当然我们也可以通过继承让其他引用类型继承EventTarget的属性和方法.
//原型式继承
var object=function(o){
    function F(){}
    F.prototype=o;
    return new F();
};
//subType继承superType的原型对象
var inheritPrototype=function(subType,superType){
    var prototype=object(superType.prototype);
    prototype.constructor=subType;
    subType.prototype=prototype;

}
function Person(name,age){
    //继承EventTarget的属性
    EventTarget.call(this);
    this.name = name;
    this.age = age;
}
//继承EventTarget的方法
inheritPrototype(Person,EventTarget);
Person.prototype.say=function(message){
    this.fire({type:'message',message:message}); //触发事件
};
//事件处理程序
var handMessage=function(event){
    alert(event.target.name + "says:" + event.message);
};
var person=new Person('yhlf',29);
person.addHandler('message',handMessage);
person.say('Hi there');
```

## javascript阻止默认行为和事件冒泡
1.阻止事件冒泡:
  event.stopPropagation();//现代浏览器
  event.cancelBubble=true;//IE浏览器
2.阻止默认行为：
  event.preventDefault();//现代浏览器
  event.returnValue=false;//IE浏览器

## 封装一个事件处理函数event
```bash
//Event工具集，from:github.com/markyunmarkyun.
Event = {
   //页面加载完成后
   readyEvent: function(fn) {
       if (fn == null) {
           fn = document;
       }
    var oldonload = window.onload;
    if (typeof window.onload != 'function') {
         window.onload = fn;
    }else{
         window.onload = function() {
            oldonload();
            fn();
         };
    }
  },
    //视能力分别使用 demo0 || demo1 || IE 方式来绑定事件
    //参数：操作的元素，事件名称，事件处理程序
    addEvent: function(element,type,handler) {
        if (element.addEventListener) { //事件类型、需要执行的函数、是否捕捉
             element.addEventListener(type,handler,false);
        }else if (element.attachEvent) {
            element.attachEvent('on' + type, function() {
                  handler.call(element);
             });
        }else {
            element['on' + type] = handler;
        }
     },
    //移除事件
     removeEvent: function(element,type,handler) {
        if (element.removeEventListener) {
             element.removeEventListener(type,handler,false);
        }else if (element.datachEvent) {
             element.datachEvent('on' + type,handler);
        }else{
             element['on' + type] = null;
        }
      },
   //阻止事件（主要是事件冒泡，因为IE不支持事件捕获）
    stopPropagation: function(ev) {
        if (ev.stopPropagation) {
             ev.stopPropagation();
        }else {
             ev.cancelBubble = true;
        }
     },
   //取消事件的默认行为
    preventDefault: function(event) {
       if (event.preventDefault) {
            event.preventDefault();
       }else{
            event.returnValue = false;
       }
    },
   //获取事件目标
   getTarget: function(event) {
      return event.target || event.srcElemnt;
   },
   //获取event对象的引用，取到事件的所有信息，确保随时能使用event；
   getEvent: function(e) {
      var ev = e || window.event;
      if (!ev) {
          var c = this.getEvent.caller;
          while(c) {
              ev = c.argument[0];
              if (ev && Event == ev.constructor) {
                   break;
              }
              c = c.caller;
          }
      }
      retrun ev;
    }
};
```
