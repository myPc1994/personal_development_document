# 移动端项目开发的配置流程
## 1、设置meta
```html
    <!-- 页面字符编码 -->
    <meta charset="utf-8">
    <!-- 避免IE使用兼容模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <!-- 启用360浏览器的极速模式(webkit) -->
    <meta name="renderer" content="webkit">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- 关键字 -->
    <meta name="keywords" content="">
    <!-- 描述 -->
    <meta name="description" content="">
    <!-- 设置移动端视图 -->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 删除苹果默认的工具栏和菜单栏 -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <!-- 设置苹果工具栏颜色 -->
    <meta name="apple-mobile-web-app-status-bar-style" content="black" />
    <!-- 忽略页面中的数字识别为电话，忽略email识别 -->
    <meta name="format-detection" content="telphone=no, email=no" />
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
```
## 2、统一页面的风格
```css
/* 防止用户自定义背景颜色对网页的影响，添加让用户可以自定义字体 */
html, body {
  height: 100%;
  width: 100%;
  overflow: hidden;
  background: #f0f0f0;
}
/*去除安卓的巨丑滚动条*/
::-webkit-scrollbar {
  display: none;
}
/* 内外边距通常让各个浏览器样式的表现位置不同 */
body, div, dl, dt, dd, ul, ol, li, h1, h2, h3, h4, h5, h6, pre, code, form, fieldset, legend, input, textarea, p, blockquote, th, td, hr, button, article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {
  margin: 0;
  padding: 0;
}
/* 要注意表单元素并不继承父级 font 的问题 */
body, button, input, select, textarea {
  font: 16px '楷体', \5b8b\4f53, arial, sans-serif;
}
input, select, textarea {
  font-size: 100%;
}
/* 去掉 table cell 的边距并让其边重合 */
table {
  border-collapse: collapse;
  border-spacing: 0;
}
/* ie bug：th 不继承 text-align */
th {
  text-align: inherit;
}
/* 去除默认边框 */
fieldset, img {
  border: none;
}
/* ie6 7 8(q) bug 显示为行内表现 */
iframe {
  display: block;
}
/* 去掉 firefox 下此元素的边框 */
abbr, acronym {
  border: none;
  font-variant: normal;
}
/* 一致的 del 样式 */
del {
  text-decoration: line-through;
}
address, caption, cite, code, dfn, em, th, var {
  font-style: normal;
  font-weight: 500;
}
/* 去掉列表前的标识，li 会继承 */
ol, ul {
  list-style: none;
}
/* 对齐是排版最重要的因素，别让什么都居中 */
caption, th {
  text-align: left;
}
/* 来自yahoo，让标题都自定义，适应多个系统应用 */
h1, h2, h3, h4, h5, h6 {
  font-size: 100%;
  font-weight: 500;
}
q:before, q:after {
  content: '';
}
i, em {
  font-style: normal;
  text-decoration: none;
}
/* 统一上标和下标 */
sub, sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
/* 让链接在 hover 状态下显示下划线 */
/*a:hover {
    text-decoration:underline;
}*/
/* 默认不显示下划线，保持页面简洁 */
ins, a {
  text-decoration: none;
}
```

## 3、使用rem来代替px
>rem 表示根元素（`<html>`）的 font-size 的大小。即如果根元素的 font-size 大小为 100px，则 1rem = 100px<br>
解决移动端分辨率碎片化的问题<br>
使用rem 自适应移动端各种分辨率（可伸缩布局方案）<br>


```javascript
/**
 * rem计算方式：设计图尺寸px / 100 = 实际rem  【例: 100px = 1rem，36px = .36rem】
 */
!function (window) {
  /* 设计图文档宽度 */
  var docWidth = 360;
  var doc = window.document,
    docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
  var recalc = (function refreshRem() {
    var clientWidth = docEl.getBoundingClientRect().width;
    /*设置最小rem的限制*/
    if (clientWidth < 360) {
      clientWidth = 360;
    }
    docEl.style.fontSize = (clientWidth / docWidth) * 100 + 'px';
    return refreshRem;
  })();
  /* 添加倍屏标识，安卓为1 */
  docEl.setAttribute('data-dpr', window.navigator.appVersion.match(/iphone/gi) ? window.devicePixelRatio : 1);
  if (/iP(hone|od|ad)/.test(window.navigator.userAgent)) {
    /* 添加IOS标识 */
    doc.documentElement.classList.add('ios');
    /* IOS8以上给html添加hairline样式，以便特殊处理 */
    if (parseInt(window.navigator.appVersion.match(/OS (\d+)_(\d+)_?(\d+)?/)[1], 10) >= 8)
      doc.documentElement.classList.add('hairline');
  }
  if (!doc.addEventListener) return;
  window.addEventListener(resizeEvt, recalc, false);
  doc.addEventListener('DOMContentLoaded', recalc, false);
}(window);
```

## 4、使用预处理语言----less
**在VUE中引入less** [教程](zh-cn/less/less.md)