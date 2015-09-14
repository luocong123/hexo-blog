title: vim常用命令
date: 2015-09-08 10:09:39
categories: blog
tags: vim
keywords: vim
---
##### 前言 
&emsp;&emsp;MAC终端terminal默认使用的是vim编辑器，经常需要上网寻找vim命令，这样就太浪费时间了，现在把一些vim常用命令纪录下。 
##### 保存
按ESC键 跳到命令模式，然后：  
```bash
:w  保存文件但不退出vi  
:w file  将修改另外保存到file中，不退出vi  
:w!  强制保存，不推出vi  
:wq  保存文件并退出vi  
:wq!  强制保存文件，并退出vi  
q:  不保存文件，退出vi  
:q!  不保存文件，强制退出vi  
:e!  放弃所有修改，从上次保存文件开始再编辑  
```
<!--more-->


