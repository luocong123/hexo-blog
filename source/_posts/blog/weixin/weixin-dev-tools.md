title: 微信公众平台开发入门之工具篇
date: 2015-09-23 18:26:32
categories: blog
tags: [微信,教程,工具]
keywords: 微信,公众平台,开发教程,ngrok,tunnel,内网穿透,QQ浏览器微信调试工具,Localtunnel
---
##### 前言
> 工欲善其事，必先利其器

##### Ngrok
微信需要外网地址，那意味着我们只能把代码传到外网服务器来查看开发调试？这样做是不是太low，而且效率及其低下，这是肯定不能接受的，下面我就介绍一个内网穿透神器ngrok，它能给我们生成一个外网地址并映射到本地服务器：  

1. 首先你要到[ngrok官网](https://ngrok.com)注册一个账户  
2. 然后[下载与系统相应的ngrok版本](https://ngrok.com/download)
3. 解压后，通过命令行进入到你解压的位置
4. 执行命令：

```bash
./ngrok authtoken <your-authtoken>
```
your-authtoken你注册后就能看到。到此ngrok就安装完成了。    
分配外网地址：

```bash
./ngrok http <your-port>
```
your-port是本地服务器端口号，可自行设置。
但上面的命令每次分配的外网地址是变化的，如果需要固定的外网地址，那你分配外网地址的时候要这样（付费用户才能用）：

```bash
./ngrok http -subdomain=<your-app> <your-port>
```
例如：./ngrok -subdomain=baz 8080，那给你分配的外网地址就是baz.ngrok.io  
<!--more-->  
**注意：ngrok 1.x与2.x命令稍有不同，请注意用ngrok －help查看**
###### ngrok使用中的问题
> 访问缓慢以及不可访问
 
由于服务器是在美国，这个稳定性实在不能保证，经常外网发布成功却不能访问或访问很慢，原因大家都懂的。 
> 域名不固定

这个你当然可以靠付费解决，ngrok并不是很贵，但结合第一条稳定性的问题，这就日了狗了。  
ngrok确实是神器，不用的话对我们开发起来确实不方便，那有解决办法么？这个是肯定的。
##### Tunnel
**关于Tunnel的最新消息：**
Tunnel不能用了，据说是[作者暂时不打算再为服务器空间续费了](http://v2ex.com/t/148279?p=2)，没钱，大家可以给你众筹嘛！不要停好不好，泪流满面有没有。因此关于Tunnel的部分可以跳过了。
    
就是这个[tunnel](http://www.tunnel.mobi/):
> tunnel是一个基于ngrok的网络服务，通过tunnel，他人在公网可以通过类似example.tunnel.mobi这样的二级域名来访问你的本地网络服务。   
tunnel部署在国内，支持ngrok的绝大多数功能，同时改变了由于ngrok服务器在美国所造成的访问缓慢和不可用的现状。

服务器在国内，域名能固定，简直完美解决了ngrok的使用问题。
###### 如何使用tunnel
1. 下载客户端：[Linux版本](https://ngrokd.b0.upaiyun.com/clients/ngrok_for_linux.zip)，[Mac OSX版本](https://ngrokd.b0.upaiyun.com/clients/ngrok_for_macosx.zip)，[32Bit Win版本](https://ngrokd.b0.upaiyun.com/clients/ngrok_for_win.zip)，[64Bit Win版本](https://ngrokd.b0.upaiyun.com/clients/ngrok_for_win_64bit.zip)
2. 下载配置文件[ngrok.cfg](https://ngrokd.b0.upaiyun.com/ngrok.cfg)
3. 运行客户端时，请添加-config以载入配置文件。

```bash
./ngrok -config ngrok.cfg -subdomain <your-appname> <your-port>
```
例如 ngrok -config ngrok.cfg -subdomain example 8080 ;意为将本地服务器的8080端口映射到example.tunnel.mobi上  
**注意：使用tunnel，需要下载的是ngrok 1.x 版本，不能是2.x版本，ngrok官方目前并不准备开放2.0客户端的第三方服务器支持**  
##### Localtunnel
[Localtunnel](http://localtunnel.me)是一个类似于ngrok的内网映射工具，但Localtunnel是基于nodejs的，而ngrok是基于go语言；相信做过一段时间前端的对nodejs都有了解的，所以安装nodejs部分略过不讲啦，当然npm也是必备的。至于为什么有了ngrok，tunnel还要用Localtunnel，实在是Tunnel虽然在国内，访问速度也可以，但经常不能访问，估计是服务器也不堪负荷，挂了，但这很耽误事好不好，好不好，好不好！只好用Localtunnel备用啦！虽然Localtunnel也不太稳定，但好待能用。好了，废话不多说。  
首先全局安装Localtunnel  

```bash
npm install -g localtunnel
```
然后设置项目名和本地服务器端口

```bash
lt -s <your-appname> -p <your-port>
```
例如：lt -s example -p 8080;意为将本地服务器的8080端口映射到example.localtunnel.me上  
**只是微信正式的公众号js接口安全域名竟然不支持未通过ICP备案的域名，真是日了狗了，日了狗了，狗了...，所以只能在[微信公众平台测试帐号](http://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login)里使用，好在测试帐号支持的接口还是比较多的**
##### QQ浏览器微信调试工具 
Tunnel挂了，localtunnel，ngrok不稳定，找一个方便的微信调试工具就迫在眉睫了，无意发现了[QQ浏览器微信调试工具](http://blog.qqbrowser.cc/wei-xin-gong-zhong-hao-ben-di-diao-shi/)，其实也是内置了使用ngrok，只是把它封装成了一个插件，粗略试了一下，还是不错的，具体教程我就不搬过来了，这里面写的很详细，只是必须下载QQ浏览器，如果不想下载QQ浏览器，可以使用网络大神从qq浏览器中提取的版本，[地址在这里](https://www.v2ex.com/t/233380),有win版和mac版，使用方式和ngrok命令一样。
###### 使用中的问题
由于使用的是8000端口，所以配置 
 
1. **网页授权获取用户基本信息（即OAuth2.0网页授权）回调页面域名**
2. **业务域名**
3. **JS接口安全域名**

需要把端口也带上,例如ul4w2.proxy.qqbrowser.cc:8000，否则会报错，当然这些都是测试帐号环境，生产环境使用80端口的话，并不需要这样