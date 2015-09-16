title: MySQL Workbench连接MySQL失败
date: 2015-09-16 14:22:27
updated: 2015-09-16 14:22:27
categories: blog
tags: [MySQL,MySQLWorkbench,MySQL客户端]
keywords: MySQL,mysql,MySQLWorkbench,连接,失败,fail,3306,127.0.0.1
---
##### 前言

>Failed to Connect to MySQL at 127.0.0.1:3306 with user root
>Can't connect to MySQL server on '127.0.0.1' (61)

今天在Mac上用[MySQL Workbench](http://dev.mysql.com/downloads/workbench/)连接mysql的时候一直报链接失败折腾几个小时，终于解决了，我觉的我是犯了经验主义的错误，现在把一些常见的可能原因列出来
##### MySQL未安装
安装MySQL Workbench并不代表你安装了MySql,它只是一个管理MySql的客户端，点这里可以[安装MySql](http://dev.mysql.com/downloads/mysql/)
##### MySQL未启动
如果你确认安装了MySQL,那可能是MySQL没有启动，你可以执行下面的命令来确认MySQL运行状态
###### 检查MySQL运行状态
```bash
sudo /usr/local/mysql/support-files/mysql.server status
```
<!--more-->  
其他相关命令：
###### 启动MySQL
```bash
sudo /usr/local/mysql/support-files/mysql.server start
```
###### 重启MySQL
```bash
sudo /usr/local/mysql/support-files/mysql.server restart
```
###### 停止MySQL
```bash
sudo /usr/local/mysql/support-files/mysql.server stop
```
**注意:** 以上操作如果需要输入密码，那个密码你登录系统时的密码，不是MySQL的密码，如果不做特别说明的话，则为MySQL的密码。
##### 端口错误
经常使用MySQL的人根据经验都会认为它的默认端口是3306，但也有可能不一样哦，我的就是3307，这也是我一直连不上的原因，因为端口不对，所以如果连不上MySQL真的需要确认一下这个端口，在确认MySQL已安装并启动的情况下执行命令
###### 第一步：在命令模式下登录MySQL
```bash
/usr/local/mysql/bin/mysql -u root -p
```
需要输入密码
###### 第二步：查看端口
```bash
SHOW GLOBAL VARIABLES LIKE 'PORT';
```
得到端口值

```bash
| Variable_name | Value |
+---------------+-------+
| port          | 3307  |
```
填写正确的端口值就OK啦
##### 密码不正确
MySQL默认账户密码是root/root,如果修改了密码却忘记了的，可以使用下面的命令来修改密码：

```bash
/usr/local/mysql/bin/mysqladmin -u root password <your-password>
```
##### 总结
当然出现连接失败的原因会有很多很多，这里列举的只是一点点，如果以后有遇到连接不上MySQL的问题也会添加但这里，以供参考。
##### 资料
[Cannot connect to MySQL Workbench on mac](http://stackoverflow.com/questions/26344795/cannot-connect-to-mysql-workbench-on-mac-cant-connect-to-mysql-server-on-127)