title: "libiconv arm移植"
date: 2015-04-25 16:54:56
categories: arm移植
tags: [arm, 移植, 动态库]
---
#libiconv
This library provides an iconv() implementation, for use on systems which don't have one, or whose implementation cannot convert from/to Unicode.

#下载
http://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.14.tar.gz
或者到这里：http://download.csdn.net/detail/chinaeran/8631163

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**目标路径：**./lib/.libs/libiconv.so.2.5.1