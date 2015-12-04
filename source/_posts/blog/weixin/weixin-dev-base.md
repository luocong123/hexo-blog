title: 微信公众平台开发入门之基础篇
date: 2015-09-22 18:26:32
categories: blog
tags: [微信,教程]
keywords: 微信,公众平台,开发教程
---
##### 前言
> 话说微信公众平台的开发文档，看着完全找不着北好吧，完全不适合新手学习嘛，最起码弄个简单入门嘛！ —— 白岩松

其实我也是个新手，写这篇也是边学边写，尽量为大家趟出一条快速入门的小道吧。当然，本篇不是教你怎样在微信公众号后台配置自动回复等简单功能的，而是完成更复杂的接口调用。
##### 准备
为什么要用微信公众平台？现在谁都能看出来移动互联网是大趋势，而开发app的成本很高，而用微信公共号营销，不仅成本小，而且迭代快，当然就成了拽住移动互联网尾巴的第二选择。

废话不多说了，微信公众号共分为三种
> 订阅号

订阅号被放在二级目录，要先点订阅号入口，才能看到订阅号列表，订阅号每天可以群发一条消息，一个月可以群发30条，总体来说订阅号偏向于媒体运营和信息传播。
> 服务号

服务号会像跟其他人的聊天信息一样放在会话列表中，服务号因为更偏重服务，所以对开发者支持也比较多，例如微信支付等订阅号不能支持的功能，但服务号不能天天发消息，一个月只能发4条，服务号侧重于对用户进行服务。
> 企业号

企业号顾名思义则是供企业内部使用，侧重于生产运营管理
<!--more-->
具体怎么选择看需求，可以参考：  
[微信公众平台服务号、订阅号的相关说明](http://kf.qq.com/faq/120911VrYVrA130805byM32u.html)  
[企业号与服务号、订阅号的区别](http://kf.qq.com/faq/140806zARbmm140826M36RJF.html)
##### 申请测试账号
可能你开发时暂时没有公众号，或者公众号正在运营，不可能让你叮叮当当的实验，没关系，我们可以申请测试账号：  
[微信公众平台接口体验测试号申请](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login)
#####  接口配置
![图1](http://7xlm9s.com1.z0.glb.clouddn.com/weixin/weixin-dev-primary-1-01.png)  
以测试账号为例，appID,appsecret由系统自动生成，我们可以先不用管，我们需要填的是URL,Token两个字段，URL即你的服务器地址，必须是一个公网地址，例如weixin.×××.com等；Token字段可以随意填入一串字符串，例如weixin，weixinfor×××等，这个算是一个私钥吧，后台必须要验证这个字段，以确定访问的合法性。
##### 服务器验证
即你部署在你的公网地址下的服务代码，咱们先不来复杂的，第一步先要把微信公众号和你的服务器建立连接吧，[微信公众平台开发者文档](http://mp.weixin.qq.com/wiki/17/2d4265491f12608cd170a95559800f2d.html)提供了一段php代码的实例：

```php
private function checkSignature()
{
	$signature = $_GET["signature"];
	$timestamp = $_GET["timestamp"];
	$nonce = $_GET["nonce"];	  		
	$token = TOKEN;
	$tmpArr = array($token, $timestamp, $nonce);
	sort($tmpArr, SORT_STRING);
	$tmpStr = implode( $tmpArr );
	$tmpStr = sha1( $tmpStr );	
	if( $tmpStr == $signature ){
		return true;
	}else{
		return false;
	}
}
```
开发者提交信息后，微信服务器将发送GET请求到填写的服务器地址URL上，GET请求携带四个参数，下面是参数说明：  

参数      |描述     
:-------:|:------:
signature | 微信加密签名，signature结合了开发者填写的token参数和请求中的timestamp参数、nonce参数。
timestamp | 时间戳
nonce	   | 随机数
echostr	| 随机字符串