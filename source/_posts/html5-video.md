---
title: html5-video控件设置
date: 2017-02-20 13:15:56
tags:
      - video
categories: html
---

### 控制Html5 Video的播放与暂停状态.
```
//Play/Pause control clicked
 $('.btnPlay').on('click', function() {
    if(video[0].paused) {
       video[0].play();
    }
    else {
       video[0].pause();
    }
    return false;
 };
```
### 显示视频播放时间和持续时间
```bash
//get HTML5 video time duration
video.on('loadedmetadata', function() {
   $('.duration').text(video[0].duration);
});

//update HTML5 video current play time
video.on('timeupdate', function() {
   $('.current').text(video[0].currentTime);
});
```
### 视频进度条
```bash
//get HTML5 video time duration
video.on('loadedmetadata', function() {
   $('.duration').text(video[0].duration));
});

//update HTML5 video current play time
video.on('timeupdate', function() {
   var currentPos = video[0].currentTime; //Get currenttime
   var maxduration = video[0].duration; //Get video duration
   var percentage = 100 * currentPos / maxduration; //in %
   $('.timeBar').css('width', percentage+'%');
});

var timeDrag = false;   /* Drag status */
$('.progressBar').mousedown(function(e) {
   timeDrag = true;
   updatebar(e.pageX);
});
$(document).mouseup(function(e) {
   if(timeDrag) {
      timeDrag = false;
      updatebar(e.pageX);
   }
});
$(document).mousemove(function(e) {
   if(timeDrag) {
      updatebar(e.pageX);
   }
});

//update Progress Bar control
var updatebar = function(x) {
   var progress = $('.progressBar');
   var maxduration = video[0].duration; //Video duraiton
   var position = x - progress.offset().left; //Click pos
   var percentage = 100 * position / progress.width();

   //Check within range
   if(percentage > 100) {
      percentage = 100;
   }
   if(percentage < 0) {
      percentage = 0;
   }

//Update progress bar and video currenttime
$('.timeBar').css('width', percentage+'%');
video[0].currentTime = maxduration * percentage / 100;
};
```
### 进阶-显示缓冲栏
```bash
//loop to get HTML5 video buffered data
var startBuffer = function() {
   var maxduration = video[0].duration;
   var currentBuffer = video[0].buffered.end(0);
   var percentage = 100 * currentBuffer / maxduration;
   $('.bufferBar').css('width', percentage+'%');

   if(currentBuffer < maxduration) {
      setTimeout(startBuffer, 500);
   }
};
setTimeout(startBuffer, 500);
```
### 音量控制
```bash
//Mute/Unmute control clicked
$('.muted').click(function() {
   video[0].muted = !video[0].muted;
   return false;
});
//Volume control clicked
$('.volumeBar').on('mousedown', function(e) {
   var position = e.pageX - volume.offset().left;
   var percentage = 100 * position / volume.width();
   $('.volumeBar').css('width', percentage+'%');
   video[0].volume = percentage / 100;
});
```
### 快进/快退 倒带控制
```bash
//Fast forward control
$('.ff').on('click', function() {
   video[0].playbackrate = 3;
   return false;
});

//Rewind control
$('.rw').on('click', function() {
   video[0].playbackrate = -3;
   return false;
});

//Slow motion control
$('.sl').on('click', function() {
   video[0].playbackrate = 0.5;
   return false;
});
```
### 其他除了主要的控制插件.还可以做一些额外的控制.例如全屏播放
```bash
$('.fullscreen').on('click', function() {
   //For Webkit
   video[0].webkitEnterFullscreen();

   //For Firefox
   video[0].mozRequestFullScreen();

   return false;
});
```
### 开灯关灯控制
```bash
$('.btnLight').click(function() {
   if($(this).hasClass('on')) {
      $(this).removeClass('on');
      $('body').append('<div class="overlay"></div>');
      $('.overlay').css({
         'position':'absolute',
         'width':100+'%',
         'height':$(document).height(),
         'background':'#000',
         'opacity':0.9,
         'top':0,
         'left':0,
         'z-index':999
      });
      $('#myVideo').css({
         'z-index':1000
      });
   }
   else {
      $(this).addClass('on');
      $('.overlay').remove();
   }
   return false;
});
```
