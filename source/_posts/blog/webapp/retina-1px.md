title: webapp retina下1px边框实现
date: 2015-12-16 10:55:18
updated: 2015-12-16 10:55:18
categories: blog
tags: [webapp,retina,1px边框]
keywords: webapp retina 1px边框 实现
---
##### 基础知识
###### 设备像素（物理像素）
显示器最小的物理显示单元。每个像素有自己的颜色、亮度。
###### 屏幕密度（PPI）
每英寸有多少像素（PPI）。当一个显示屏像素密度超过300ppi时，人眼就无法区分出单独的像素。PPI高于210（笔记本电脑）、260（平板电脑）、300（手机）的屏幕都称为Retina屏幕。
###### CSS像素（设备独立像素，dips）
CSS像素主要使用在浏览器上，就是写CSS时使用的像素px，CSS像素在所有屏幕上是一样的，与设备无关。
###### 设备像素比 window.devicePixelRatio(dpr)
window.devicePixelRatio = 物理像素/设备独立像素（dips）  
非视网膜的dpr=1，CSS 1px 对应一个物理像素，如：非视网膜屏幕的手机，dpr=320/320=1  
视网膜的dpr=2，CSS 1px 对应四个物理像素，如：视网膜屏幕的手机，dpr=640/320=2。1个CSS像素对应2*2=4个物理像素  

<!--more-->
retina下，物理像素要1px，那CSS像素就得是0.5px，不然看上去会粗。
##### 解决方案
###### 设border-width为小数
现在IOS8和IOS8以上版本，已经支持小数边框了，那么意味着，我们可以使用如下的css代码

```css
.hairlines * { border-width: .5px !important; }
```
但这样子IOS8以下的版本，以及android浏览器都不支持，会把边框border-width:0,就没有边框啦。所以如果使用这个方案最好做一下优雅降级，即对不支持的版本还使用原来的边框。  
js判断UA

```js
if (/iP(hone|od|ad)/.test(navigator.userAgent)) {
  var v = (navigator.appVersion).match(/OS (\d+)_(\d+)_?(\d+)?/),
    version = parseInt(v[1], 10);
  if(version >= 8){
    document.documentElement.classList.add('hairlines')
  }
}
```
或者js判断是否支持0.5px边框，是的话，则输出类名hairlines

```js
if (window.devicePixelRatio && devicePixelRatio >= 2) {
  var testElem = document.createElement('div');
  testElem.style.border = '.5px solid transparent';
  document.body.appendChild(testElem);
  if (testElem.offsetHeight == 1){
    document.querySelector('html').classList.add('hairlines');
  }
  document.body.removeChild(testElem);
}
```
###### scale
可以用1px尺寸的带背景色元素然后scaleX(0.5)或scaleY(0.5)实现0.5px效果。

```css
/*下边框1px*/
.hairlines{    
    position: relative; 
} 
.hairlines:after{    
    content: '';    
    position: absolute;    
    bottom:0;    
    left:0;    
    right:0;    
    border-bottom:1px solid #dadada;    
    -webkit-transform:scaleY(.5); 
    transform:scaleY(.5);   
    -webkit-transform-origin:0 0;
    transform-origin:0 0;  
}

/*四边框实现*/
.hairlines{    
    position: relative; 
    border-radius: 8px;
    border: none;
} 
.hairlines:after{
    content: '';
    position: absolute;
    top: 0;
    left: 0;    
    width: 200%;
    height: 200%;
    border: 1px solid #dadada;
    border-radius: 8px;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;   
    -webkit-transform: scale(.5);
    transform: scale(.5);
    -webkit-transform-origin: left top;
    transform-origin: left top;
}
```
这种方案目前来说是一个不错的解决方案,操作方便，而且对圆角有一定的支持，兼容性也算可以。  
如果加一个判断是否Retina屏，来确定是否使用这种方式创建边框那当然是最好啦

```js
if(window.devicePixelRatio && devicePixelRatio >= 2){
  document.querySelector('html').classList.add('hairlines');
}
```