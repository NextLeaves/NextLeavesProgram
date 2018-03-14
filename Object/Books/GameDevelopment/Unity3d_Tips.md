---

title: Unity Tips
date: 3/14/2018 00:00:00 AM 
tags:
- tip
- unity3d
categories: unity3d
thumbnail: 

---

# Unity3d开发小技巧 #

* Wrote : 3/14/2018 00:00:00 AM 
* Name  : NextLeaves

* 1. 工具类
	* 时间
	* 等待
	* 随机数
	* 数学
	* 四元数

---

## 1. 工具类 ##

### 1.1 时间 ###

* **Time**类
	* 属性：
		* time
		* deltatime：Update()完成上一帧消耗的时间
		* fixedTime：FixedUpdate()固定消耗的时间总和
		* fixedDeltaTime：固定更新上一帧所消耗的时间

### 1.2 等待 ###

* 实现类：**WaitForSeconds()**
* 注意问题：返回值一定是**IEnumerator**类型

·

	IEnumerator Test()
	{
		Debug.Log(Time.time);
		yield return new WaitForSeconds(2);
		Debug.Log(Time.time);
	}
	
### 1.3 随机数 ###

* Unity内置的：
	* **Random**类 --- 属性：Range()；有整型，有浮点
* C#内置的：
	* **Random**类 --- 属性：Next()；（同理上）

* 冲突问题：
	* 对于同时引入ns（namespace），使用全称修饰访问

### 1.4 数学 ###

* **Mathf**类
	* 行为：
		* Abs()
		* Clamp()
		* Lerp()
		* Sin()
		* Cos()
		* Tan()
		* Max()：返回两个值的最大值
		* MIn()：返回两个值的最小值
		* PI：圆周率

### 1.5 四元数 ###		

* **Quaternion**类
	* Slerp()：插值算旋转度
	* Euler()：欧拉公式，