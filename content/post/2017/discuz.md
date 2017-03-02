---
categories:
- 技术文档
date: 2017-02-16T10:48:32+08:00
description: "Discuz"
keywords:
- xxx
title: Centos7下Discuz搭建
url: ""
---

废话不多说直接进去主题，我们先在Discuz官方论坛将源码下载下来 [Discuz](http://download.comsenz.com/DiscuzX/3.3/Discuz_X3.3_SC_UTF8.zip)
这里为了方便我直接给出了下载地址。如果有最新版本可以直接去官网去下载。
接下来我们将配置安装环境：  
### 1.首先安装环境所需软件
Appache,Mariadb(以前叫mysql,现在开源的服务名叫Mariadb),php，php-mysql(后续安装界面如没安装此服务会报错) 
### 2.安装以上服务开启前关闭防火墙（firewall）及 Selinux
* 关闭firewall防火墙   
临时关闭：systemctr stop firewalld  
禁止开机启动：systemctr disable firewalld
![](./images/FirewalldStop.png)
* 关闭Selinux（后续要没关闭此服务文件不可写入）  
临时关闭：setenfore 0    
永久关闭：修改配置文件/etc/selinux/config,将其中selinux设置为disable  
![](./images/SelinuxDisable.png)
### 3.接下来就安装所需软件
* 安装Appache服务(本文中已安装)  
查看是否已安装：yum list | grep httpd 或者 yum list installed | grep httpd 或者 rpm -qa | grep httpd  
![](./images/httpd.png)  
**注：最后一列标记有@base的表示已安装**  
![](./images/httpd1.png)  
如未安装请使用：yum -y install httpd  
* 安装Mariadb-server数据库   
使用 yum -y install mariadb-server.x86_64 安装完成后查询是否已安装 yum list | grep mariadb  
![](./images/mariadb.png)
* 安装php , php-mysql
yum -y install php php-mysql安装后如下图：  
![](./images/php.png)
### 4.上传下载好的安装包里的upload文件到linux的/var/www/html目录下
解压下载好的安装包，将里面upload文件上传到/var/www/html目录下，本例使用xftp工具来上传。  
![](./images/up.png)  
使用cd/var/www/html进入到html目录下，将upload目录及其子目录更改权限 chmod -Rf 777 upload/(根据具体情况授予权限)   
![](./images/chmod.png)

### 5.启动httpd和mariadb服务
* 开启httpd和mariadb服务  
systemctl start httpd , systemctl start mariadb  
查看服务状态：    
![](./images/httprun.png)
![](./images/mariadbrun.png)
* 开机启动httpd和mariadb服务  
systemctl enable httpd , systemctl enable mariadb  
查看开机启动状态：  
![](./images/httpAndMariadbEnable.png)
### 6.打开浏览器输入：http://ip/upload(ip是你服务器的ip地址)
如下图出现安装界面接下来就按提示下一步安装：  
![](./images/discuzInstall.png)
![](./images/install.png)
![](./images/install_01.png)
![](./images/install_02.png)
![](./images/install_03.png)
![](./images/install_04.png)
![](./images/install_05.png)
### 7.安装完毕
之后可以进入管理员界面进行模块创建与管理了





