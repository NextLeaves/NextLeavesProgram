---

title: cpt 13 Optimize Unity Game
date: 3/3/2018 10:50:08 AM 
tags: 
- script
categories: unity3d
thumbnail: https://i.imgur.com/4vwkwsO.jpg

---

# 第十三章 Unity3d游戏优化 #

* Wrote : 3/3/2018 10:50:10 AM 
* Name  : NextLeaves

* CPU优化
* 物理组件优化
* 内存优化
* 代码优化
* GPU优化

---

## 1. unity3d游戏优化入手目标 ##

* **Draw Call**是一个必须要提的概念
	* 何为此？**DrawCall**是对底层图形程序(OpenGL)的调用，CPU去调用(CPU作为中央处理器，接受程序的指令)
* **fragment**有可能成为像素的东西
	* 属于**vf**，**v**指的是vertex；**f**就指的fragment
	* 对于GPU有所影响
* **Batching**将需要多次调用的图像接口的物品组合在一起，然后再一起调用一次接口
* **内存分配**
	* unity3d自带的内存损耗
	* Mono带有的损耗
	* 托管的那一些东西
	* 引入自己的几个dll文件
* 优化注意的三个方面：
	* 1. CPU
	* 2. GPU
	* 3. 内存

## 2. CPU方面的优化 ##

* 影响CPU效率的方面：
	* 1. DrawCall
	* 2. 物理组件(physics)
	* 3. GC
	* 4. 脚本的代码质量

### 2.1 对DrawCall的优化 ###

* 底层接口调用需要处理许多事情，所以尽量组合需要一起渲染的物体，一起调用底层接口，减少cpu对底层接口的调用
	* 1. DrawCallBatching，unity3d在运行时，会组合可以一起调用渲染的物体，减少DrawCall次数
	* 2. 把纹理打包成图集，减少材质的使用
	* 3. 尽量少的使用反光、阴影之类的效果，因为那会使物体多次渲染
* 使用Draw Call Batching功能
	* 1. 针对于为什么使用**不同材质**的物体，即使使用了此方法，也无法达到性能提醒，调用次数的下降
		* a. 因为不同的材质，决定了使用了不同的纹理，导致所需的物体不同，导致接口调用的内容不同，即使调用，也无法达到优化的效果
		* b. 只有使用相同的材质，使用相同的纹理，才能使用此功能，达到应有的效果
		* c. 对于使用的不同纹理的材质，可以将纹理打包成图集，然后使用同一个材质，达到此方法调用的目的
	* 2. 分为两种：static batching , dynamic batching
		* static batching：针对于无需移动，同时使用相同材质的物体，达到整合的效果；只需要在物体的static勾选即可
		* dynamic batching：
			* 此机制是由Unity引擎所进行的，在生成对象的时候，会自动的进行**batching**操作
			* 针对动态批处理还有部分的约束：（举例：生成prefab的scale不一样，也会导致**batching**失效）
				* a. 动态批处理需要在每个顶点有一定开销，所以仅支持小于900顶点的网格物体
				* b. 如果着色器使用顶点位置、法线、UV值三种属性，则只能支持300顶点以下的物体
				* c. 若着色器使用顶点位置，法线，UV0,UV1和切向量，那么只支持180顶点以下的物体
				* d. 统一缩放的物体，会进行批处理
				* e. 使用不同材质的物体，不会进行批处理
				* f. 多通道的shader会妨碍批处理操作
				* g. 拥有lightingmap的物体含有额外的材质属性

### 2.2 对物理组件优化 ###

* 1. 针对**Fixed Timestep**的优化使用：
	* 此为FixedUpdate的调用次数，通过cpu计算达到模拟物理效果
	* 选择合适的值，尤为重要，对优化有一定缓解
* 2. 针对**Mesh Collider**的优化使用：
	* 勾选convex的组件，可以和其他组件发生效果，但是其开销过大，但精确度高，这就需要权衡游戏的需要

### 2.3 处理内存，却放CPU受伤的GC ###	

* 1. GC意为Garbage Collection，垃圾回收器
	* GC的影响？作为在堆上面没有引用的数据会被GC所释放；但是是通过CPU进行操作的，加重CPU负担；
	* 什么会被GC释放？存储在堆上的引用类型（比如，类类型，字符串等），像int、float等则为值类型
	* GC何时会触发？
		* 针对此，C#的GC管理器，会把堆对象分为多级成员，每次判断失去引用的堆数据，会进行释放
		* 内存不足时
		* 程序员可以手动调节GC
	* 减少触发GC，从根本优化CPU负担：
		* a. 字符串的连接，实则为生成第三个字符串，然后赋值，前两个则为垃圾
		* b. foreach语句会涉及迭代器，据说每一次循环所产生的24bytes的垃圾
		* c. 使用gameobject.CompareTag("human"),而不是if(gameobject.tag=="human");后者会生成tag的垃圾
		* d. 使用“池”，实现资源复用
		* e. 最好不使用LINQ命令

### 2.4 对代码质量的优化 ###			

* 1. 若频繁使用某个对象，则可以保存对象的实例；而不是频繁调用获取
* 2. 不要频繁使用GetComponent()
* 3. 使用内建数组；Vector.zero，而不是new Vector(0,0,0);
* 4. 善用OnBecameVisible()和OnBecameInvisible()来控制Update的执行
* 5. ref参数的使用

## 3. 对GPU的优化 ##