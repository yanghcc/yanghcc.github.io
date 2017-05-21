---
title: css笔记
date: 2017-02-18 16:21:58
categories:  css
---

#### css实现自适应正方形
/*img外层*/
``` bash
.img-wrap{
     width: 100%;
     padding: 50% 0;
    height: 0;
    border: none;
    background: none;
    text-align: center;
    position: relative;
    overflow: hidden;
}
```
/*img使用绝对定位*/
``` bash
.img-wrap img{
     width: 100%;
     position: absolute;
     top: 0;
     left: 0;
}
```
/*css3将图片裁剪并居中，需要给img标签设置固定宽高*/
``` bash
.img-wrap img{
     width: 100%;
     height: 100%;
     object-fit: cover;
}
```
#### 文本内容禁止选中
```bash
.disable-selected{
          -moz-user-select: -moz-none;
          -moz-user-select: none;
          -o-user-select:none;
          -webkit-user-select:none;
          -ms-user-select:none;
          user-select:none;
     }
```

#### 去除ios系统表单元素默认内阴影
``` bash
-webkit-appearance:none;
```
注：适用于表单元素 input && textarea
#### flex学习笔记
```bash
display:flex;
justify-content:flex-end;居右
justify-content:center;居中
justify-content:space-between;左右对齐  《水平方向》
align-items:center;垂直居中
align-items:flex-end;居底    《垂直方向》
flex-direction:cloum;设置排列方向为竖直方向
对于子元素：item{ align-self: center; }则是根据自身属性进行定位。
```
#### css透明度被继承的问题
使用rgba():
```bash
.bg{
    background:rgba(0,0,0,0.3)
}
/*代替*/
.bg{
    background-color:#000;
    opacity:.3;
}
```
```bash
background: rgb(0, 0, 0);    /*不支持rgba的浏览器*/
background: rgba(0,0,0,.5);  /*支持rgba的浏览器*/
filter:progid:DXImageTransform.Microsoft.gradient(startColorstr=#7f000000,endColorstr=#7f000000);    /*IE8支持*/
```

#### 移动端，超过两行的高度，显示省略号
```
.ellipsis{
    overflow : hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
}
```

#### js去除首尾空格
```bash
//去除字符串两端空格的方法，string是全局对象
String.prototype.noSpace=function(){
    return this.replace(/^\s*|\s*$/g, '');
  }
```

#### 根据请求头，判断设备类型，重新定向链接
```bash
var u = navigator.userAgent;
     if (u.indexOf('Android') > -1 || u.indexOf('Linux') > -1
               || u.indexOf('Windows Phone') > -1 || u.indexOf('iPhone') > -1
               || u.indexOf('iPad') > -1) {
               window.location.href ='http://m.anta.cn/';

     }
```

#### 记录常见浏览器兼容Q&A
1、浏览器默认的margin和padding不同。解决方法：
```bash
*{margin:0;padding:0;}
```
2、IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。解决方法：
```bash
display:inline;//在float的标签display属性转化为行内属性。
```
3、在ie6，ie7中元素高度超出自己设置高度。原因是IE8以前的浏览器中会给元素设置默认的行高的高度导致的。解决方案是加上overflow:hidden或设置line-height为更小的高度。

4、min-height在IE6下不起作用。解决方法：
```bash
height:auto!important;
height:xxpx;其中xx就是min-height设置的值。
```
5、透明性IE用filter:Alpha(Opacity=60)，而其他主流浏览器用 opacity:0.6;

6、a(有href属性)标签嵌套下的img标签，在IE下会带有边框。解决办法:
```bash
a img{border:none;}
```
7、input边框问题。去掉input边框一般用border:none;就可以，但由于IE6在解析input样式时的BUG(优先级问题)，在IE6下无效。   ie6的默认CSS样式，涉及到border的有border-style:inset;border-width:2px;浏览器根据自己的内核解析规则，先解析自身的默认CSS，再解析开发者书写的CSS，达到渲染标签的目的。IE6对INPUT的渲染存在bug，border:none;不被解析，当有border-width或border-color设置的时候才会令IE6去解析border-style:none; 解决方案如下，推荐用第三种方案:
```bash
方法一：
border:0
方法二：
border:0 none;
方法三：
border:none:border-color:transparent;
```
8、父子标签间用margin的问题，表现在有时除IE(6/7)外的浏览器子标签margin转移到了父标签上，IE6&7下没有.

9、父子关系的标签，子标签浮动导致父标签不再包裹子标签。解决方法是清楚浮动,多种方法如下：
```bash
/* bootstrap解决办法 */
.clearfix:before,
.clearfix:after{
    content: "";
    display: table;
}
.clearfix:after{
    clear: both;
}
.clearfix{
    zoom:1;
}
/* zoom是在处理兼容性问题，hidden和auto都能清除浮动，据说auto对seo更友好 ，缺点：多级结构时*/
.clear-float3{ overflow: auto/hidden; zoom: 1; }

/*当父包含块缩成一条时无效 */
.clear-float1{ content: “”; display: block; clear: both; }

/*兄弟级别加一个空div。 */
.clear{clear:both; height: 0; line-height: 0; font-size: 0}
```

10、列出display的值，说明他们的作用。
解：block 象块类型元素一样显示。none 缺省值。象行内元素类型一样显示。inline-block 象行内元素一样显示，但其内容象块类型元素一样显示。list-item象块类型元素一样显示，并添加样式列表标记。

11、position的值， relative和absolute定位原点是？
解：*absolute 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。*fixed（老IE不支持）生成绝对定位的元素，相对于浏览器窗口进行定位。*relative 生成相对定位的元素，相对于其正常位置进行定位。 * static  默认值。没有定位，元素出现在正常的流中 *（忽略 top, bottom, left, right z-index 声明）。* inherit 规定从父元素继承 position 属性的值。