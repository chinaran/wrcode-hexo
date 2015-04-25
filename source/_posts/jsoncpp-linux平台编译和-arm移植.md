title: "jsoncpp linux平台编译和 arm移植"
date: 2015-04-25 18:17:40
categories: arm移植
tags: [arm, 移植, 动态库]
---
#jsoncpp
soncpp is an implementation of a JSON (http://json.org ) reader and writer in C++. JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate.

#下载
http://sourceforge.net/projects/jsoncpp/
或者到这里：http://download.csdn.net/detail/chinaeran/8631141

#Linux平台编译
解压后运行如下命令：

    # 先安装 scons
	$ sudo apt-get install scons
	$ scons platform=linux-gcc

**目标路径：**
动态库：./libs/linux-gcc-4.8/libjson_linux-gcc-4.8_libmt.so
静态库：./libs/linux-gcc-4.8/libjson_linux-gcc-4.8_libmt.a

#arm平台编译
**注**：platform 没有包含 arm 平台，类似 linux-gcc，所以把源码提取出来，独立编译
解压后运行如下命令：

	$ mkdir arm_jsoncpp
	$ cp include/ arm_jsoncpp/ -r
	$ cp src/lib_json/* arm_jsoncpp/
	$ cd arm_jsoncpp/
	
	# 编译静态库
	$ arm-linux-gnueabihf-g++ -c *.cpp -I./include -fPIC
	$ ar cr libjsoncpp.a *.o
	
	# 编译动态库
	$ arm-linux-gnueabihf-g++ -shared -fPIC *.cpp -I./include -o libjsoncpp.so
	
**目标路径：**
动态库：./arm_jsoncpp/libjsoncpp.so
静态库：./arm_jsoncpp/libjsoncpp.a