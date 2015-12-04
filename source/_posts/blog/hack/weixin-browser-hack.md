title: 微信浏览器hack记录
date: 2015-12-01 14:26:17
updated: 2015-12-01 14:26:17
categories: blog
tags: [h5,hack,weChat,browserhack,weixinbrowserhack]
keywords: 微信浏览器hack,hack  
---
##### 微信浏览器文本框不能输入内容
###### 原因
在h5开发中，为了禁掉用户可以选中页面中的内容，你可能使用了一下css属性值：

```css
-webkit-user-select: none;
user-select: none;
```
这个属性将导致微信内置浏览器文本框不能输入内容，注意并不仅仅在微信浏览器有这个问题，ios自带游览器，百度浏览器似乎也有这个问题，uc浏览器表现正常
###### 解决办法
1. 尽量不要再全局使用属性，只给需要的元素添加这个属性
2. 如果必须在全局使用属性，那可以给不需要的元素，看情况添加以下值：

> auto—默认值，用户可以选中元素中的内容  
text—用户可以选择元素中的文本  
all—在编辑器内，如果双击/上下文点击发生在子元素上，改值的最高级祖先元素将被选中。

如：

```css
-webkit-user-select: auto;
user-select: auto;
```
