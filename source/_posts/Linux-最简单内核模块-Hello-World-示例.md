title: "Linux 最简单内核模块 Hello World 示例"
date: 2015-04-27 14:31:34
categories: driver
tags: [kernel, driver]
---
**注：**如果想要按照本篇实践，需要有能运行的arm开发板和对应版本的内核（也可参考其他文章直接在Linux主机上编译运行）

###1. 在相应版本内核的driver目录下新建如下文件：
![module file tree][1]

其中文件代码如下：
/\* **hello.c** \*/

    #include <linux/init.h>
	#include <linux/module.h>

	static int hello_init(void)
	{
		printk(KERN_INFO "[init] Can you feel me?\n");
		return 0;
	}

	static void hello_exit(void)
	{
		printk(KERN_INFO "[exit] Yes.\n");
	}


	module_init(hello_init);
	module_exit(hello_exit);

	MODULE_AUTHOR("Alan Wang <alan@wrcode.com>");
	MODULE_LICENSE("GPL");
	MODULE_DESCRIPTION("A simple Hello World Module");
	MODULE_ALIAS("A simple module");

/\* **Kconfig** \*/

    # drivers/alan_test/Kconfig

	menu "ALAN_TEST Driver "
	comment "ALAN_TEST Driver comment"

	config ALAN_TEST
		bool "ALAN_TEST support"

	config HELLO
		tristate "hello module test"
		depends on ALAN_TEST

	endmenu

/\* **Makefile** \*/

    # drivers/alan_test/Makefile
	# makefile for the ALAN_TEST

	obj-$(CONFIG_HELLO)	+= hello.o

###2. 修改上一级目录的 Kconfig Makefie：
drivers 下的 Kconfig 末尾 endmenu 前添加一行

    source "drivers/alan_test/Kconfig"

    endmenu

drivers 下的 Makefile 末尾加一行

    obj-$(CONFIG_ALAN_TEST)		+= alan_test/

###3. make menuconfig 添加刚写好的模块到内核：
依次是：Device Drivers  --->
　　　　　ALAN_TEST Driver   --->
　　　　　　　\*\*\* ALAN_TEST Driver comment \*\*\*
　　　　　　　[*] ALAN_TEST support<M>
　　　　　　　< M >　hello module test

退出**保存** menuconfig

###4. 编译内核：
使用 **make** 编译
生成的 **zImage** (arch/arm/boot/zImage) 烧写到开发板对应位置。
生成的 **hello.ko**(drivers/alan_test/hello.ko) 复制到开发板Linux系统的一个目录下。

###4. 插入内核模块：
![insmod][2]

###5. 使用 modinfo 查看模块信息：
![modinfo][3]

  [1]: /images/Linux-最简单内核模块-Hello-World-示例/1.png
  [2]: /images/Linux-最简单内核模块-Hello-World-示例/2.png
  [3]: /images/Linux-最简单内核模块-Hello-World-示例/3.png