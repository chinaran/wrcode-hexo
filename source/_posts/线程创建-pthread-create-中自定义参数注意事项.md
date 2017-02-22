title: "线程创建 pthread_create 中自定义参数注意事项"
date: 2017-02-10 07:54:32
categories: Linux C
tags: [linux, C]
---

 **1. 函数原型**
int **pthread_create**(pthread_t *thread, const pthread_attr_t *attr,
　　　　　　　　　void *(*start_routine) (void *), void *arg);
本文主要讨论最后一个参数，同时传递多个的问题
（如果只传递一个 int char 等长度小于指针的数据类型，可以直接传，然后在线程内把 (void *) 强制转换）

 **2. 错误示例**
是在一本书上看到的，也是写本文的初衷

![线程创建错误参数传递示例][1]

错误原因：<!-- more -->
fds_for_new_worker 是局部变量，线程创建异步的，pthread_create 后, else if 也结束了，该变量的生命周期结束，worker 线程访问到的将是野指针，容易造成数据访问错误或更严重的内存错误。

 **3. 正确传递方法**
A. 使用全局变量（视情况使用）
　变量的作用域不会消失，但要注意多线程变量同步问题
B. 动态分配变量空间(推荐)
　在 pthread_create 前 malloc() 申请空间，在线程内使用完后 free()

 **附：错误代码验证**

	#include <stdio.h>
	#include <string.h>
	#include <stdlib.h>
	#include <unistd.h>
	#include <pthread.h>

	struct data_st
	{
		int a;
		int b;
	};

	static void *start_routine(void *user)
	{
		// sleep(1);
		struct data_st *data = (struct data_st *)user;
		printf("in thread, data->a = %d, data->b = %d\n", data->a, data->b);

		pthread_detach(pthread_self());
		return NULL;
	}

	int main(void)
	{
		int i;
		int ret;
		pthread_t pt;

		for (i = 0; i < 5; ++i)
		{
			struct data_st data;
			data.a = i;
			data.b = i * 2;

			ret = pthread_create(&pt, NULL, start_routine, &data);
			if (0 != ret)
			{
				printf("%s(): Thread creation failed\n", __FUNCTION__);
				exit(EXIT_FAILURE);
			}
		}

		pause();
		
		return 0;
	}

运行结果：
![运行结果][2]
可以看出，这种错误的传递方式并没有得到应有的结果

  [1]: /images/线程创建-pthread-create-中自定义参数注意事项/线程创建错误参数传递示例.png
  [2]: /images/线程创建-pthread-create-中自定义参数注意事项/运行结果.png
