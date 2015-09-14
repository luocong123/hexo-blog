title: Mac下Maven配置
date: 2015-09-14 09:51:53
updated: 2015-09-14 09:51:53
categories: blog
tags: [Maven,java,构建工具]
keywords: Maven,java,构建工具,Maven安装教程,Maven配置
---
##### 下载Maven
[下载最新版本Maven](http://maven.apache.org/download.cgi)  
下载后放置在一个目录，写这篇文章时最新版本为3.3.3，所以我把它放在了Documents/maven-3.3.3，当然这不是强制的，可自定义
##### 设置环境变量
使用Maven需要设置环境变量，Mac系统本质是Linux，因此Linux设置环境变量的办法，通常也适用于Mac. 一般来讲，有3个地方可以设置环境变量:  
> /etc/profile  

全局配置，不管是哪个用户，登录时都会读取该文件  
> ~/.bashrc  

全局配置，bash shell执行时，不管是何种方式，都会读取此文件，一般在这个文件中添加系统级环境变量
> ~/.bash_profile  
    
一般在这个文件中添加用户级环境变量, 所以最好是修改.bash\_profile文件  
<!--more-->
###### 打开终端，输入命令
```bash
open ~/.bash_profile
```
如果习惯vim或者nano编辑也可以直接在终端打开
###### 编辑
```bash
export M3_HOME=/Users/luocong/Documents/maven-3.3.3
export PATH=$PATH:$M3_HOME/bin
```
注意把M3_HOME目录替换成你自己的  
###### 立即生效
```bash
source ~/.bash_profile
```
注意环境变量设置后并不会立即生效，需执行以上命令才能生效
###### 验证
```bash
mvn –version
```
出现类似于Apache Maven 3.3.3的信息即为成功
##### 常见问题
执行mvn –version报错：
> Maven Installation OSX Error Unsupported major.minor version 51.0

出现这个错误一般是java版本过低，不支持所安装的Maven版本，或者是java升级后，没有配置环境变量（升级并不会自动配置JAVE_HOME到最新版本）  
解决方法：  
1. 升级java  
2. 配置JAVA\_HOME如下   
```bash
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_76.jdk/Contents/Home
export M3_HOME=/Users/luocong/Documents/maven-3.3.3
export PATH=$PATH:$M3_HOME/bin:$JAVA_HOME/bin
```
注意自行修改jdk版本
