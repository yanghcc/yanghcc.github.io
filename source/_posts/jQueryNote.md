---
title: jQueryNote
date: 2017-02-20 19:50:34
tags:
      - javaScript
      - jQuery
categories: javaScript
---

### jquery trigger()源码
```
/**
   * 事件触发器
   * @param { Object } DOM元素
   * @param { String / Object } 事件类型 / event对象
   * @param { Array }  传递给事件处理函数的附加参数
   * @param { Boolean } 是否冒泡
 **/
  trigger : function( elem, event, data, isStopPropagation ){
      var type = event.type || event,
          // 冒泡的父元素，一直到document、window
          parent = elem.parentNode ||
              elem.ownerDocument ||
              elem === elem.ownerDocument && win,
          eventHandler = $.data( elem, type + 'Handler' );

      isStopPropagation = typeof data === 'boolean' ?
          data : (isStopPropagation || false);

      data = data && isArray( data ) ? data : [];

      // 创建自定义的event对象
      event = typeof event === 'object' ?
          event : {
              type : type,
              preventDefault : noop,
              stopPropagation : function(){
                  isStopPropagation = true;
              }
          };

      event.target = elem;
      data.unshift( event );
      if( eventHandler ){
          eventHandler.call( elem, data );
      }
     // 递归调用自身来模拟冒泡
      if( parent && !isStopPropagation ){
          data.shift();
          this.trigger( parent, event, data );
      }
  }
```

### 封装一个核心函数，实现类jquery的链式调用
```bash
  /*
    函数库封装，创建一个核心对象。Ice
   */
    var $ = function(){
      return new Ice();
    };
  function Ice(){
    //创建一个数组来保存获取的节点和节点数组
    this.elem = [];
    //获取elem的id
    this.getId=function(obj){
      obj = obj.noSpace();
      if(obj.substring(0,1)=="#"){
      nobj = obj.substring(1);
      nobj = document.getElementById(nobj);
      this.elem.push(nobj);
      return this;
      }
    }
    //获取元素elem的class
    this.getClass=function(obj){
      obj = obj.noSpace();
      if(obj.substring(0,1)=="."){
      nobj = obj.substring(1);
      nelem = document.getElementsByClassName(nobj);
      for (var i=0; i < nelem.length; i++) {
        this.elem.push(nelem[i]);
      }
      return this;
      }
    }
  }
  //定义css()方法
  Ice.prototype.css=function(attr,val){
    for (var i=0; i < this.elem.length; i++) {
      if (arguments.length==1) {
        if (typeof window.getComputedStyle != "undefined"){//W3C
          return window.getComputedStyle(this.elem[i],null)[attr];
        }else if(typeof this.elem[i].currentStyle != "undefined"){//IE
          return this.elem[i].currentStyle[attr];
        }
        return this.elem[i].style[attr];
      }
      this.elem[i].style[attr] = val;
    }
    return this;
  }
  //定义html()方法
  Ice.prototype.html=function(str){
    for (var i=0; i < this.elem.length; i++) {
      if (arguments.length==0) {
        return this.elem[i].innerHTML;
      }
      this.elem[i].innerHTML = str;
    }
    return this;
  }
  //定义click()方法
  Ice.prototype.click=function(fn){
    for (var i=0; i < this.elem.length; i++) {
      this.elem[i].onclick = fn;
    }
    return this;
  }
  //定义addClass()方法
  Ice.prototype.addClass=function(className){
    className = className.noSpace();
    var reg = new RegExp('(\\s|^)'+className+'(\\s|$)');
    for (var i=0; i < this.elem.length; i++) {
      if (!this.elem[i].className.match(reg)) {//判断类名是否存在，不存在则添加
        this.elem[i].className += ' '+className;
      }
    }
    return this;
  }
  //定义removeClass()方法
  Ice.prototype.removeClass=function(className){
    className = className.noSpace();
    var reg = new RegExp('(\\s|^)'+className+'(\\s|$)');
    for (var i=0; i < this.elem.length; i++) {
      if (this.elem[i].className.match(reg)) {//判断类名是否存在，存在则删除,即用空格替代
        this.elem[i].className = this.elem[i].className.replace(reg,' ');
      }
    }
    return this;
  }
  //定义eq()方法
  Ice.prototype.eq=function(num){
    var elems = this.elem[num];
    this.elem = [];//清空元素数组
    this.elem[0] = elems;
    return this;
  }
  //定义first()方法
  Ice.prototype.first=function(){
    var elems = this.elem[0]
    this.elem = [];//清空元素数组
    this.elem[0] = elems;
    return this;
  }
  //定义last()方法
  Ice.prototype.last=function(){
    var la = this.elem.length-1;
    var elems = this.elem[la];
    this.elem = [];//清空元素数组
    this.elem[0] = elems;
    return this;
  }
```
### 封装document对象cookies方法
```bash
 sessionStorage.setItem()&sessionStorage.getItem();
 localStorage.setItem()&localStorage.getItem();
```
//参数解析：
name:cookie名 val:cookie值 expires:cookie过期时间 path:有效路径 domain:有效域名 secure:是否加密
```bash
function setCookie(name,val,expires,path,domain,secure){
  var cookieName = encodeURIComponent(name)+"="+encodeURIComponent(val);
  if(expires instanceof Date){//setting expries day time
    cookieName +=";expires="+expires;
  }
  if (path) {
    cookieName +=";path="+path;//setting cookie path
  }
  if (domain) {
    cookieName +=";domian="+domain;//setting proxy name
  }
  if (secure) {
    cookieName +=";secure";//setting secure
  }
  document.cookies = cookieName;
};

function setCookieDate(day){ //get day function
  var date = null;
  if(typeof day == "number" && day>0){
    date = new Date();
    date.setDate(date.getDate()+7);
  }else{
    throw new Error("你的天数不合法！请设置数字");
  }
  return date;
}
setCookie("user","yang");
setCookie("url","icetower.cn",setCookieDate(7));

//获取cookies值
function getCookie(name){
  var cookieName = encodeURIComponent(name)+"=";
  var cookieStart = document.cookies.indexOf(cookieName);
  var cookieVal = null;
  if(cookieStart > -1){
    var cookieEnd = document.cookies.indexOf(";",cookieStart);
    if (cookieEnd == -1) {
      var cookieEnd = document.cookies.length;
    }
    var val=document.cookies.substring(cookieStart+cookieName.length,cookieEnd);
    cookieVal=decodeURIComponent(val);
  }
  return cookieVal;
};
// console.log(getCookie("user"));
// console.log(document.cookies);
```

### jquery点击空白，隐藏弹窗面板
```bash
$(document).mouseup(function(e){
    var _con = $(".tartet");   // 设置目标区域
    if(!_con.is(e.target) && _con.has(e.target).length === 0){
      $(".tartet").hide();
    }
  });
  ```