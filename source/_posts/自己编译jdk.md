title: 自己编译jdk8
author: Halfopen
tags:
  - java基础
  - ''
categories:
  - java
date: 2017-11-20 20:52:00
---
系统：centos7
OpenJDK：OpenJDK 8

## 获取源码
安装Mercurial代码版本管理工具

	sudo apt-get install mercurial

下载源码

	hg clone http://hg.openjdk.java.net/jdk8/jdk8
	cd jdk8

我们按其中的README-builds.html 进行操作

	sudo chmod 775 get_resource.sh
	./get_resource.sh
    
要下载的代码如下：

|Repository |	Contains|
|:--:|:---|
|. (root) 	|common configure and makefile logic|
|hotspot 	|source code and make files for building the OpenJDK Hotspot Virtual Machine|
|langtools |	source code for the OpenJDK javac and language tools|
|jdk 	|source code and make files for building the OpenJDK runtime libraries and misc files|
|jaxp 	|source code for the OpenJDK JAXP functionality|
|jaxws 	|source code for the OpenJDK JAX-WS functionality|
|corba 	|source code for the OpenJDK Corba functionality|
|nashorn |	source code for the OpenJDK JavaScript implementation |
一定要确定上面所有库都下载完成后才进行下一步

检测环境依赖

	sudo chmod 775 configure
	./configure
结果如下

![upload successful](\assets\images\自己编译jdk\pasted-0.png)

按提示安装

	sudo apt-get install libx11-dev libxext-dev libxrender-dev libxtst-dev libxt-dev libcups2-dev libfreetype6-dev libasound2-dev ccache

其中，libX11-dev我改为了libx11-dev

再次运行	./configure ,结果如下

![upload successful](\assets\images\自己编译jdk\pasted-1.png)

## 编译源码


![upload successful](\assets\images\自己编译jdk\pasted-2.png)