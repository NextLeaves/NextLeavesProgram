---

title: cpt 5 Observer Pattern
date: 3/5/2018 10:14:31 AM 
tags:
- designpattern
- csharp
categories: designpattern
thumbnail: https://i.imgur.com/WiBfKkJ.jpg

---

# 第二章 观察者模式 #

* Wrote : 3/5/2018 10:14:46 AM  
* Name  : NextLeaves

* 气象监测站的设计
* 鸭子、老鼠、猫的故事
* 五分钟短剧-观察的主题
* 定义观察者模式
* 办公室的隔间对话
* 最终规划气象站
* 围炉夜话
* Java内置的OB模式

---

## 1. 气象监测站的设计 ##

* 1. 支持扩展的天气预报系统
	* 接收来自WeatherData对象获取的数据
	* 三种内容：
		* 目前状况
		* 气象统计
		* 简单预报
* WeatherData类-源代码

`

	class WeatherData:
	{
		getTemperature();
		getHumidity();
		getPressure();
		measuremetnsChanged();//设计人员外留的接口
	}

* 我们应该知道的内容：
	* 1. 当数据更新时，就会调用最后一个外留接口方法
	* 2. WeatherData类有三个方式获取对应的气象值
	* 3. 调用接口后，我们要同步更新我们设计的三个面板的数据值
	* 4. 设计的面板还支持自定义功能，便于用户自定义设计

### 1.1 错误范例 ###

`

	void MeasurementsChanged()
	{
		float temperature = getTemperature();
		float humidity = getHumidity();
		float pressure = getPressure();
	
		currentConditionDisplay.update(temperature,humidity,pressure);
		```;
		```;
	}

### 1.2 讲解观察者模式 ###

* 1. 以报社的角度来思考，观察者模式（出版社为Subject，订阅者为Observer）
* 2. 以小动物的角度来思考，观察者模式
* 3. 以HR纳才的角度来思考

## 2. 定义观察者模式 ##

* **定义了对象之间一对多的依赖关系，当主题对象的状态发生改变的时候，订阅了的对象会收到通知并且自动更新**
* Subject接口：具有**注册，移除，通知**三大主要方法
* Observer接口：具有**更新**主要方法
* 设计原则：**为了对象之间的松耦合设计而努力。**

## 3. 具体的设计类图 ##

* 1. 首先以接口编程为原则；WeatherData类继承Subject接口，其他的面板继承Observer接口，扩展显示接口为ShowElement接口
* 2. 实现响应的方法：
	* Subject接口具有三大方法：
		* register()
		* remove()
		* notify()
	* Observer接口具有方法：
		* update()
	* ShowElement接口具有的方法：
		* show()