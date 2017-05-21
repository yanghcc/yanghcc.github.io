---
title: canvas笔记
date: 2017-02-20 16:28:31
tags:
     - html5
     - canvas
categories: html
---

```
window.onload = function(){//页面加载完执行

var canvas = document.getElementById(“id”);//获取canvas元素
var context = canvas.getContext(“2d”);//调用canvas绘图接口，设置绘图的上下文环境
var convas.width = x;
var convas.height = x;//设置canvas画布大小
var img = new Image();//重新定义一个图片对象

img.onload = function(){//图片加载完成后执行
    var img.width = convas.width;
    var img.height = canvas.height;//设置图片大小和canvas画布同样大小

    drawImage(img,0,0);//根据图片自身大小直接绘制图形，drawImage()总共三种调用方式如下
    drawImage(img,dx,dy,img.width,img.height);
    drawImage(img,sx,dy,img.width,img.height,dx,dy,canvas.width,canvas.height);//(sx,sy)是原图像起点坐标、(dx,dy)是目标 图像起点坐标
}

context.beginPath()//开始本次绘制标识

context.clearRect(0,0,canvas.width,canvas.height);//清除整个画布，参数值为画布起点坐标和大小
context.save();//保存画布

context.arc(x,y,r,0,2Math*PI,false);//绘制一个圆形，(x，y)是圆心，r是半径，0是起始点，2π是结束点，默认fasle是按顺时针方向绘图

var clippingRegion = {x:400,y:400,r:50};//定义裁剪区域
context.arc(clippingRegion.x,clippingRegion.y,clippingRegion.r,0,Math.PI*2,false);//绘制裁剪区域
context.clip();//将除了arc规定的这个区域以外的内容的全部剪掉
context.restore();//画布恢复

context.fillStyle = “color”;//图形填充颜色
context.fill();//执行填充

context.moveTo(x,y);//绘制线条起点位置坐标
context.lineTo(x,y);//绘制线条结束位置坐标
context.lineWidth = 10;//线条宽度
context.lineCap = “butt";//默认，值还可以是“round”,突出圆形头，或者“square”，突出方形头
context.lineJoin =“miter";//默认值尖角，“bevel”使用斜接的形式过度,”round”使用圆角形式过度
context.miterLimit = 10;默认值，线条交接处，角度尖锐程度

context.strokeStyle = “color”;//线条颜色
context.stroke();//绘制线条

content.rect(x,y,width,height);//绘制正方形
content.fillRect();
content.strokeRect();

context.closePath()//结束本次绘制标识

// var lGrd = context.createLinearGradient(0, 0, 400, 400);//创建线性渐变
// lGrd.addColorStop(0, '#ff0000');
// lGrd.addColorStop(1, '#0000ff');
// context.fillStyle = lGrd;
// context.fillRect(0, 0, 400, 400);//填充区域的起始点和宽高
// var rGrd = context.createRadialGradient(600, 200, 100, 600, 200, 200);//创建径向渐变
// rGrd.addColorStop(0, '#ccc');
// rGrd.addColorStop(1, '#333');
// context.fillStyle = rGrd;
// context.fillRect(400, 400, 400, 400);

/* 图形变换的方法，记得成对使用save()&&restore()方法，保存canvas绘图状态，保证图形变换后不会出错 */
context.save();//保存画布
context.translate(x,y);//平移的方法
context.rotate(deg);//旋转的方法
context.scale(x,y);//x轴和y轴缩放比例，注：scale会同时缩放外边框，左上角坐标值等副作用
context.restore();//画布恢复

}
```
