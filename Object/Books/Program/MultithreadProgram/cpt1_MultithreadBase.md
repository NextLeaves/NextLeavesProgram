---

title: cpt 1 Multithreading Base
date: 2018/1/11 22:47:52
tags:
- multithreading
- csharp
categories: program
thumbnail: https://i.imgur.com/Sp4wwei.jpg

---

# 第一章 多线程基础 #

* Wrote : 2018/1/11 22:47:52
* Name  : NextLeaves

* C#中基本的线程操作

---

## 1.1 线程的创建 ##

* 名称空间：using System.Threading;
* 引用类：using static System.Threading.Thread;（C#6.0用法，引入Thread的静态函数，属性）
* Thread类---实例化类---参数为函数名

## 1.2 暂停线程 ##

* 意义：暂停线程的操作，暂停时刻不占有计算机资源
* 实例函数：**.Sleep(Timespan.FromSeconds(2000))**

## 1.3 线程等待 ##

* 意义：有约束的线程操作，直到线程执行完后才进行后续操作，在之前一直处于阻塞状态
* 实例函数：**.Join()**

## 1.4 终止线程 ##

* 意义：立刻结束线程的执行，对于停掉线程的操作很有必要
* 实例函数：**.Abort()**
	* 实际是：向线程注入**ThreadAbortException()**函数，导致线程终止
	* 但，线程可以处理异常，如调用**Thread.ResetAbort()**函数，可以不停止操作
* 推荐使用一下方法**终止线程**：
	* 传入**CancellationToken()**方法，具体第三章会涉及到

## 1.5 检测线程状态 ##

* 意义：在处理、操作线程时候，应判断线程的状态，再进行具体的操作
* 实例属性：**.ThreadState**

## 1.6 线程优先级 ##

* 意义：优先级决定线程能够获得计算机获得多少的资源
* 实例属性：**.Priority**
	* 枚举：ThreadPriority
		* Highest
		* Lowest

## 1.7 前台线程和后台线程 ##

* 意义：应用在关闭的时候，前台线程必须全部执行完才能结束应用；后台线程可以在任何时候进行中断
* 实例属性：**.IsBackground**

## 1.8 向线程传递参数 ##

* 意义：可以动态的向线程传递参数，便于处理主线程的数据
* 两种传参方法：
	* **第一种：**嵌套函数，调用函数的参数为Object类型的参数；再进行转换参数；在Start()函数中进行传参
	* **第二种：**使用Lambda表达式，嵌入所需调用的函数，但Lambda为无参的函数
		* Lambda表达式所遇两种问题：
			1. 传入的是常量，或者固定的值，不影响线程的执行
			2. 传入的是变量，此时会产生一种问题，**闭包问题**
				* 被捕获的变量，将在IL中生成一个临时存储的数据类型，然后不会在*作用域**里面重置、删除变量值

## 1.9 C#中的lock关键字 ##

* 意义：处理多线程中竞争问题，竞争条件是多线程中导致应用程序处理失败的原因
* 实质：是**Monitor类**的一个语法糖

`

	//语法糖的书写方式
	public readonly Object _sync = new Object();
	lock(_sync)
	{
		count++;
	}

	//实际Monitor类书写方式
	bool requiredLock=false;
	try
	{
		Monitor.Enter(_sync,ref requiredLock)
		{
			//implement
		}
	}
	finally
	{
		if(requiredLock)Monitor.Exit(_sync);
	}
	
## 2.10 Monitor类锁定资源 ##

* 意义：在多线程中，资源的同时操作会导致数据错误，所以保证资源在同一时间只有一个线程进行操作是很有必要的，但是lock嵌套操作等，会造成**死锁**问题
	* 造成**死锁**的四个条件：
		* 竞争条件
		* 循环等待
		* 请求等待
		* 不剥夺（此乃操作系统机制，无法改变）
	* 解决死锁问题，从前三个方面着手考虑，Monitor类，就是此处存在的意义

`

	//Monitor类使用方法
	lock(object2)
	{
		if(Monitor.TryEnter(object1,TimeSpan.FromSeconds(5)))
		{
			//获取资源后处理成功
		}else
		{
			//未获取资源失败，跳出等待条件
		}
	}

	//死锁状态
	//若一直无法获取object1的使用权限，则造成死锁，程序终止运行
	lock(object2)
	{
		lock(object1)
		{
			//获取资源后处理成功
		}
	}

## 2.11 在多线程中处理异常 ##

* 意义：在多线程中遇到错误，需要进行异常处理的情况下；主线程是无法捕获其他线程的异常的，所以在该线程操作块里面进行try.catch操作是很有必要的
* 在.NET1.0和1.1中，应用程序不会因为未捕获异常而导致程序崩溃

`

	//更改配置文件
	<configuration>
		<runtime>
			<legacyUnhandledExceptionPolicy enabled="1" />
		</runtime>
	</configuration>