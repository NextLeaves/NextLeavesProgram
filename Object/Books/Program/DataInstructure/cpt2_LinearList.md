---

title: cpt 2 Linear List
date: 2/28/2018 2:08:20 PM  
tags:
- data
- structure
categories: structure
thumbnail: ![](https://i.imgur.com/6JTaj3C.jpg)

---

# 第二章 数据结构 #

* Wrote : 2/28/2018 2:08:20 PM  
* Name  : NextLeaves

* 线性表的逻辑结构
* 顺序存储和链式存储

---

## 1 线性表的逻辑结构 ##

### 1.1 线性表的基本操作 ###

* 1. 初始化、销毁
* 2. 查找
* 3. 存取
* 4. 插入、删除
* 5. 排序、求长度、判空

### 1.2 顺序表的实现 ###

* 关键字：
	* **#define**：用于声明常量；如 **#define INIT_SIZE 100**
	* **typeof**：用于类型别名；如 **typeof int ElemType**
	* **typeof struct{}SqList;**：声明结构体格式
* 线性表的初始化：
	* malloc(byte size)：实现分配存储空间，参数为分配存储空间大小；如INIT_SIZE*sizeof(int)，分配的空间强制转换为int类型，(int *)
	* 思考逻辑：
		* 1. 是否分配成功；判断指针是否为空
		* 2. 然后初始化各项其他字段
* 线性表的插入：
	* 思考逻辑：
		* 1. 判断插入位置是否合法
		* 2. 判断线性表是否满
			* 1. 若满，则remalloc(int origin,int size)分配新的空间
			* 2. 再判断是否为空
		* 3. 进行插入操作
			* 1. 后移元素
			* 2. 插入值
			* 3. 更改其他字段参数
		* 4. 完成插入，返回链表指针
* 线性表的删除：
	* 逻辑思考：
		* 1. 判断删除位置是否正确
		* 2. 执行删除操作
		* 3. 进行移动元素操作
		* 4. 完成删除操作
* 线性表的查找：
	* 逻辑思考：
		* 1. 使用while进行操作，或者for
			* 注意点：只要判断while中为true|false既可以获取导出的位置内容