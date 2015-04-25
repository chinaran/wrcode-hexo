title: "json-c arm移植"
date: 2015-04-25 17:35:42
categories: arm移植
tags: [arm, 移植, 动态库]
---
#json-c
JSON-C implements a reference counting object model that allows you to easily construct JSON objects in C, output them as JSON formatted strings and parse JSON formatted strings back into the C representation of JSON objects.

#下载
https://github.com/json-c/json-c
或者到这里：http://download.csdn.net/detail/chinaeran/8630977

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

    # autoconf automake libtool 必须安装好
    $ sudo apt-get install autoconf
    $ sudo apt-get install automake
    $ sudo apt-get install libtool

    $ ./autogen.sh
	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**目标路径：**./.libs/libjson-c.so.2.0.0