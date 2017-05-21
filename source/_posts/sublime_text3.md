---
title: sublime text3开发环境
date: 2017-02-22 10:49:15
tags:
     - sublime
     - IDE
categories: others
---

## sublime text3开发环境搭建，常用插件整理
sublime是我最喜欢的编辑器，简约高效、轻便灵活、功能插件丰富.
### 注册码：
—– BEGIN LICENSE —–
Michael Barnes
Single User License
EA7E-821385
8A353C41 872A0D5C DF9B2950 AFF6F667
C458EA6D 8EA3C286 98D1D650 131A97AB
AA919AEC EF20E143 B361B1E7 4C8B7F04
B085E65E 2F5F5360 8489D422 FB8FC1AA
93F6323C FD7F7544 3F39C318 D95E6480
FCCC7561 8A4A1741 68FA4223 ADCEDE07
200C25BE DBBC4855 C4CFB774 C5EC138C
0FEC1CEF D9DCECEC D3A5DAD1 01316C36
—— END LICENSE ——

### 常用设置：
设置自动保存："save_on_focus_lost": true,
设置默认缩进："tab_size":2
...
<img src="/images/user_setup.png" alt="set">

### 常用插件
```bash
安装package control       # tool菜单下选中package control
安装 emmet                # 编码快捷键 //前端神器 !important
安装 jsformat             # js代码格式化
安装 LESS                 # 代码高亮
安装 alignment            # 对齐变量等号
安装 sublime-autoprefixer # 自动补充浏览器兼容前缀
安装 Bracket Highlighter  # 自动代码匹配
安装 jQuery               # jq代码提示
安装 Doc​Blockr            # 代码注释美化 //!important
安装 AutoFileName         # 自动补全文件名 //!important
安装 Trailing spaces      # 去除多余空格 //强迫症福音
安装 git                  # git管理
安装 ColorPicker          # 颜色提取 //!important
安装 File Header          # 新建文件时，自动创建文件头信息(开发者，时间等等)
安装 rem-unit             # 移动端开发神器，px单位自动转rem单位（需设置根字体大小）
安装 CSScomb              # 也是神器，可按照设置，重新排序css代码
安装 sublime server       # sublime服务环境
深空灰主题 spacegray       # 深空灰主题
海军蓝主题 Materrial Theme # 精美的主题，推荐
安装 Trmmer               # 代码格式化和对齐
安装 JsMinifier           # 该插件基于Google Closure compiler，自动压缩js文件。
安装 QuoteHTML            # 让js代码中插入html代码片段变得简便
安装 emmet liveStyle      # 安装后还需要谷歌浏览器安装一个liveStyle插件，浏览器启动插件后，在开发者工具里调整样式直接会保存在源文件。同时源文件修改样式，会自动刷新浏览器页面。太方便了
...
```
常用的插件都简单介绍了一下，还有几个插件安装后没有显示。例如：Vuejs Snippets / vue syntax highLight / react-native-snippets 等等。提高基于vue / react-native框架开发的效率。
其中，emmet插件已经配置好微信小程序常用代码片段。如果需要使用我的sublime配置环境，可以到我的github拷贝,[传送门](https://github.com/yanghcc/User).有使用方法描述

效果图：
<img src="/images/sublime.png" alt="img">
<img src="/images/plugins.png" alt="img">

补充：
Webstorm 16.3激活教程。在打开的License Activation窗口中选择“License server”，在输入框输入下面的网址点击,点击Activate即可。
```bash
http://idea.iteblog.com/key.php
```