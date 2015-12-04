title: UC浏览器hack记录
date: 2015-10-16 11:06:34
updated: 2015-10-16 11:06:34
categories: blog
tags: [UC,hack,UCbrowserhack]
keywords: UC浏览器hack,hack  
---
##### uc浏览器网页字体被放大
###### 原因
uc浏览器会对wap页面字体按规则放大
###### 解决办法
若不想页面字体被放大，可以通过增加html5标签header、nav、section中的任一个来避免,如在body中添加header空标签：

```html
<body>
<header></header>
...
</body>
```