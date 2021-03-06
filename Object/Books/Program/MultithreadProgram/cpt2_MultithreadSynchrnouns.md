---

title: cpt 2 Multithreading Synchrnouns
date: 2018/1/17 14:37:03 
tags:
- multithreading
- csharp
categories: program
thumbnail: https://i.imgur.com/Sp4wwei.jpg

---

# 第二章 多线程同步操作 #

* Wrote : 2018/1/17 14:37:03
* Name  : NextLeaves

* C#中基本的线程同步处理方式

---

## 2.1 简介 ##

* 同步的四种解决方式：
	* 原子模式
		* 只是使用短暂的处理事件，不用阻塞其他线程的处理，但是针对于原子的处理方式是数学中的逻辑加减和乘除算法等函数体
		* 个人理解：对于计算机来说，原子级的处理事件，即可忽略的十分短的时间
	* 内核模式
		* 即切换其他线程，即取消线程对cpu资源的占用，可大大提高目标线程的处理速度和减少相应时间；
		* 但是，挂起线程，会使cpu在其之前进行**上下文切换（context switch）**，保存阻塞线程的当前状态，并且切换到目标线程的过程，使其咱有cpu资源，如果阻塞时间长，其效果是显著的，反之则不推荐
		* 当阻塞时间不长，推荐使用用户模式，虽然咱有cpu资源，浪费cpu时间，但是其切换效率是迅速的
		* 只有Windows的内核才具有挂起线程的权限，即线程调度器
	* 用户模式
		* 当不需要太多时间的挂起，则可以使用阻塞的方式
		* 只是浪费cpu时间，未处理未使用的状态，但是切换的速度快
	* 混合模式
		* 根据阻塞的时间长度来动态的选择改变模式
		* 先尝试使用**用户模式**，若阻塞时间过长，则采用**内核模式**

## 2.2 原子模式 ##

* 用对象实现基本的原子操作，从而不阻塞其他线程达到避免**竞争条件**
* **用法：**
	1. 对数据进行操作的时候，调用**Interlocked类**的静态方法
	2. Interlocked类
		* 静态方法：
			* Increment()
			* Decrement()
			* Add()

## 2.3 Mutex类 ##

* 是一种原始的同步方式（互斥体）
* 使线程具有独占资源的能力（类似于给以线程一把钥匙，然后进行访问，使用完后返还钥匙）
* **用法：**
	1. 生成一个Mutex类的对象，即“钥匙体”，需要传入string参数
	2. Mutex类：
		1. 对象方法：
			* WaitOne()：实现获取钥匙，若获得返回true，反之false
			* ReleaseMutex()：释放Mutex对象，即“钥匙体”
* **注意：**
	* Mutex类生成的对象是一个全局对象，需要注意使用完之后一定要释放；推荐使用**using语句**生成

## 2.4 SemaphoreSlim类 ##

* 是一种根据初始化的数量，来判定资源可以共享的线程数目
* **用法：**
	* 生成**Semaphore类**的对象，初始化为设置多少个线程可以共享
	* 当需要使用时，需要分配资源是否未占满**.Wait()**
	* 对象方法：
		* .Wait()：分配资源位置
		* .Release()：释放资源位置 
* **注意：**
	1. Semaphore类是SemaphoreSlim的老版本
	2. 前者为内核模式，后者为混合模式
	3. 后者不使用windows的内核信号量，也不支持进程间同步功能
	4. 跨进程同步的场景，前者较为合适

## 2.5 AutoResetEvent类 ##

* 从一个线程向另一个线程发送通知的方式
* 告诉另一个线程将有事情发生
* **用法：**
	* 生成两种事件对象：workEvent、mainEvent
	* 对象方法：
		* .Set()：发送信号
		* .WaitOne()：等待通知
* **注意：**
	* 采用内核模式

## 2.6 ManualResetEvent类 ##

* **意义：**具有更加的性能和方式，相较于AutoResetEvent类
* **用法：**
	* 生成对象
	* 对象方法：
		* .Set()：打开大门，需要的直接进入
		* .Reset()：关闭大门，无法进入，即阻塞操作

## 2.7 CountDownEvent类 ##

* 信号类，判断达到一定的信号数目才继续执行
* **用法：**
	* 生成对象，初始化为多少个信号数目的获取
	* 对象方法：
		* .Signal()：发送该任务完成的信号
		* .Wait()：等待信号数目够，然后继续执行
* **注意：**
	* 信号数目如果一直不够，将一直处于阻塞状态；确保一定能发送足够的信号数目

## 2.8 Barrier类 ##

* **意义：**组织多个线程在某个时刻碰面，之后调用回调函数
* **用法：**
	* 生成对象，初始化包括回调函数内容（Action<>）
	* 对象方法：
		* .SignalAndWait()：等待线程碰头
* **注意：**
	* 多线程迭代运算十分合适，在一次迭代运算之后，进行测试，调用回调函数进行判断

## 2.9 ReaderWriterLockSlim类 ##

* **意义：**针对于对象资源的读取与写的控制，可以使多线程能够同时进行读操作，但是对于写操作只能独占写方式
* **用法：**
	* 生成对象
	* 对象方法：
		* .EnterReadLock()：执行共享读取操作
		* .EnterWriteLock()：执行独占写操作
		* .ExitReadLock()：退出共享读操作
		* .ExitWriteLock()：退出独占写操作
		* .EnterUpgradeableReadLock()：升级读操作的方式；为了在读操作的时候，若遇到写操作，继续获取读锁
		* .ExitUpgradeableReadLock()：同上，退出操作
* **注意：**
	* 升级锁的方式，是为了在获取读锁的时候，若遇到写锁，若未升级锁（即未使用EnterUpgradeableReadLock()），将先获取写锁，再获取读锁，这样会造成读锁进行阻塞，导致信息获取延迟
	* 为了避免时间的浪费，同时又不需要及时更新的值，那么可以使用升级锁的方式来操作
	* 尽可能的使用try..catch操作

## 2.10 SpinWait类 ##

* 不使用内核模式的，线程等待操作（混合模式）
* **用法：**
	* 生成对象
	* 对象方法：
		* .SpinOnec()：跳转次数，当操作9次后，将切换内核模式
	* 对象属性
		* .NextSpinWillYield：获取当前跳转次数
* **注意：**
	* **volatile：**确保修饰的字段不会被编译器处理为单线程处理，可以被多线程同时处理，保证值的最新
	* 9此迭代后。将切换为内核模式