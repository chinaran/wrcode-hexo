title: "libpcap arm移植"
date: 2015-04-25 17:57:04
categories: arm移植
tags: [arm, 移植, 动态库]
---
#libpcap
a portable C/C++ library for network traffic capture.

#下载
http://www.tcpdump.org/#latest-release
或者到这里：http://download.csdn.net/detail/chinaeran/8631799

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux

**报错**如下：
configure: **error:** pcap type not determined when cross-compiling; use --with-pcap=... follow**
**解决**方法：
将 configure 文件中的如下内容注释掉

	# if test -z "$with_pcap" && test "$cross_compiling" = yes; then
	#     as_fn_error $? "pcap type not determined when cross-compiling; use --with-pcap=..." "$LINENO" 5
    # fi
继续 

    $ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
    
**报错**：
configure: **error:** Your operating system's lex is insufficient to compile
 libpcap.  flex is a lex replacement that has many advantages, including
 being able to compile libpcap.  For more information, see
 http://www.gnu.org/software/flex/flex.html .
 
 **安装flex**
 
	$ sudo apt-get install flex
	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make
	
依然**报错**：
make: **yacc: Command not found**

**再安装byacc**

    $ sudo apt-get install byacc
    $ make

终于成功啦！！！
**目标路径：**./.libs/libcconv.so.0.0.0