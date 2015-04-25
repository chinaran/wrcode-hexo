title: "curl arm移植"
date: 2015-04-25 18:55:16
categories: arm移植
tags: [arm, 移植, 动态库]
---
#curl
curl is a command line tool and library for transferring data with URL syntax, supporting DICT, FILE, FTP, FTPS, Gopher, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMB, SMTP, SMTPS, Telnet and TFTP. curl supports SSL certificates, HTTP POST, HTTP PUT, FTP uploading, HTTP form based upload, proxies, HTTP/2, cookies, user+password authentication (Basic, Plain, Digest, CRAM-MD5, NTLM, Negotiate and Kerberos), file transfer resume, proxy tunneling and more.

#下载
http://curl.haxx.se/download/curl-7.41.0.tar.bz2
或者到这里：http://download.csdn.net/detail/chinaeran/8631829

#编译
**注**：此处使用 arm-linux-gnueabihf-gcc，--build 使用的是64位Linux，可以不添加此参数
解压后运行如下命令：

	$ ./configure --host=arm-linux-gnueabihf --build=i686-pc-linux
	$ make

**目标路径：**./lib/.libs/libcurl.so.4.3.0