title: "cconv arm移植"
date: 2015-04-25 17:20:16
categories: arm移植
tags: [arm, 移植, 动态库]
---
#cconv
cconv(pronunciation: see-conv.) is iconv based simplified-traditional chinese conversion tool. It is NOT only transcoding programm, but also TRANSLATE tools between the Simplified Chinese and Traditional Chinese.

#下载
https://code.google.com/p/cconv/downloads/list
或者到这里：http://download.csdn.net/detail/chinaeran/8630971

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**报错**如下：
cconv-cconv.o:/home/alan/libs/cconv/cconv-0.6.2/cconv.c:311: **more undefined references to `rpl_malloc' follow**
**解决**方法：
将 configure 文件中的 #define malloc rpl_malloc 注释掉 (-> // #define malloc rpl_malloc)

	$ make clean
	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**目标路径：**./.libs/libcconv.so.0.0.0