title: "libini arm移植"
date: 2015-04-25 17:52:53
categories: arm移植
tags: [arm, 移植, 动态库]
---
#libiconv
An INI file parser that can read, edit and create large INI files. Usable under Microsoft Windows, DOS, Linux, etc. Supported languages are C, C++, Visual Basic, Java, TCL, Perl, Python, etc (DLL and SWIG capable).

#下载
http://sourceforge.net/projects/libini/files/libini/libini-1.1.10/
或者到这里：http://download.csdn.net/detail/chinaeran/8631153

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**目标路径：**./src/.libs/libini.so.1.0.10