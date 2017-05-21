---
title: 使用vuejs开发的一个面试页面
date: 2017-03-9 19:17:02
tags:
     - vuejs
     - vue-scroller
     - momentjs
     - axios
     - xml2json.js
     - 正则表达式
categories: 前端框架
---


[试题链接](https://github.com/fuliaoyi/showmecode)

[参考答案GitHub地址](https://github.com/yanghcc/interviewTest)

演示效果：
<img src="/images/operation1.gif" alt="pic">

##### 第一部分

是关于javascript的简答题，考的是js基础知识。涉及的内容包括数组操作，js中改变this指向的方法call()以及js原型法。

##### 第二部分

使用SPA框架开发一个滚动加载的页面，我使用的是vue.js，涉及的开发知识比较多。项目核心知识包括Vue.js，webpack，vue-scroller，axios，moment.js，xml2json.js，跨域问题，JavaScript正则匹配。数据源是[http://36kr.com/feed](http://36kr.com/feed)，数据格式是xml。

#### 正文如下。大家可以看看试题，再看看我的参考答案，以下是详细介绍，欢迎大家给参考答案点一个star~

1.项目结构直接使用vue-scroller的演示demo    [传送门](https://github.com/wangdahoo/vue-scroller-demo)

2.配置webpack，设置proxy代理，解决网络请求插件axios获取[http://36kr.com/feed](http://36kr.com/feed)存在跨域问题。在webpack.config.js中devServer的设置添加proxy，如下：

```
devServer: {
    historyApiFallback: true,
    noInfo: true,
    proxy: {
        '/feed': {
        target: 'http://36kr.com/',
        changeOrigin: true,
        secure: false
      }
    }
  }
```

3.移动端使用相对长度单位rem，需要在index.html中添加一段js代码，根据屏幕尺寸设置根字体大小。

```javascript
<script type="text/javascript">
		window.addEventListener('resize', infinite);
		function infinite() {
		    const html = document.getElementsByTagName('html')[0];
		    const htmlWidth = document.body.clientWidth
		    if (htmlWidth >= 1080) {
		        html.style.fontSize = "42px";
		    } else {
		        html.style.fontSize = (42/ 1080 * htmlWidth) + 'px';
		    }
		}infinite();
  </script>
```

4.这部分知识主要包括vue指令v-for、v-if、v-text、v-html。以及自定义事件refresh、infinite。css只要使用flex布局，比较简单不贴代码了，组件html结构如下：

```html
<template>
  <div id="app">
    <scroller :on-refresh="refresh"
              :on-infinite="infinite"
              ref="my_scroller">
      <div v-for="(item, index) in items" class="row">
        <h1 class="itme-title" v-text="item.title.__cdata"></h1>
        <div class="itembox">
          <span class="author" v-text="item.author"></span>
          <span class="category" v-text="item.category"></span>
          <span class="timebox" v-text="newmoment(item.pubDate.__cdata)"></span>
        </div>
        <a class="item-content" :href="item.link">
          <div class="leftbox" v-html="handlerData(item.description.__cdata)"></div>
          <div class="rightbox">
            <div class="imgbox">
              <img class="img" :src="skewImg.url?skewImg.url:'/src/assets/404.jpg'">
            </div>
          </div>
        </a>
      </div>
    </scroller>
  </div>
</template>
```

5.在vue生命周期created阶段，通过axios发起网络请求，获取数据之后，将数据经过xml2json插件转换后，保存json数据到本地数组。

```javascript
 data() {
      return {
        items: [],//当前渲染数据
        allData: [],//所有数据
        dataLen: 0,//数据总长度
        step: 10,//上拉加载时，每次载入数据的数量
        times: 0,//上拉加载次数
        skewImg: []//缩略图保存地址
      }
    },
created() {
        var dataObj = {};
        var self = this;
        axios.get('/feed')
        .then(function (response) {
          var x2js = new X2JS();
          var dataObj = response.data;
          var jsonObj = x2js.xml_str2json( dataObj );
          var itemData = jsonObj.rss.channel.item;
          for (var i = itemData.length; i >= 0; i--) {
            self.allData.push(itemData[i])
          }
          self.dataLen = self.allData.length;
        })
        .catch(function (error) {
          console.log(error);
        });
    }
```

6.渲染到页面前数据处理，若当前item有多张图片，则保存第一张图片的src地址，若没有图片则保存一个空值。然后将数据去除所有html标签，只保留300个字符长度的文本，渲染到页面中：

```javascript
handlerData(str) {
        var self = this;
        var dd = '';
        var arr = str.replace(/<img [^>]*src=['"]([^'"]+)[^>]*>/i, function (match, capture) {
             dd = capture
        });
        self.skewImg['url'] = dd;

        var str = str.substring(0,300);
        return str.replace(/<[^>]+>/g,"");
      }
```

7.渲染到页面前，使用moment.js格式化时间。

```javascript
newmoment(arg) {
        return moment(arg).format('MM 月 DD 日 hh:mm')
	 }
```

8.上拉加载更多调用infinite()方法，每次上拉操作，次数times自加1，并往items数组添加step长度的数据：

```javascript
infinite() {
        var self = this;
        setTimeout(() => {
          self.times +=1;
          var end = ((self.step)+1)*self.times;
          var sta  = end - self.step;
          self.items = self.items.concat(self.allData.slice(sta,end));
          // console.log(self.items.length)
          if (self.items.length >= self.allData) {
            this.$refs.my_scroller.finishInfinite(true)
          }
          setTimeout(() => {
            this.$refs.my_scroller.finishInfinite(true)
          })
        }, 1500)
      }
```

9.下拉刷新调用reflesh()方法，重新发起一次网络请求，并且往items中填充step条数据：

```javascript
refresh() {
        setTimeout(() => {
        var dataObj = {};
        var self = this;
        axios.get('/feed')
        .then(function (response) {
          var x2js = new X2JS();
          var dataObj = response.data;
          var jsonObj = x2js.xml_str2json( dataObj );
          var itemData = jsonObj.rss.channel.item;
          self.items = [];//重置数据
          self.allData = [];//重置数据
          self.times = 1;//重置数据
          for (var i = itemData.length; i >= 0; i--) {
            self.allData.push(itemData[i])
          }
          self.allData.shift();//删除数组第一个数据
          var end = ((self.step)+1)*self.times;
          var sta  = end - self.step;
          self.items = self.allData.slice(sta,end);
        })
        .catch(function (error) {
          console.log(error);
        });
          if (this.$refs.my_scroller)
            this.$refs.my_scroller.finishPullToRefresh();
        }, 1500)
      }
```


最后是遗留问题：应该是webpack配置有点问题，执行build打包之后，设置的proxy代理失效。求大神帮忙看看。