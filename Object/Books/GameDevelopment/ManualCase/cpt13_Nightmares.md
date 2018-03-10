---

title: cpt 13 Nightmares
date: 3/10/2018 4:30:18 PM 
tags:
- unity3d
- 3d
categories: unity3d
thumbnail: https://i.imgur.com/ws0gAKv.jpg

---

# 第十三章 噩梦射手 #

* Wrote : 3/10/2018 4:30:21 PM 
* Name  : NextLeaves

* 新UGUI介绍
* 案例分析
	* 设置场景
	* 角色控制管理
	* 角色生命值管理
	* 角色射击和敌人生命值管理
	* 游戏分值的显示和敌人对象的动态创建
	* 结束游戏

---

## 1. 新uGUI介绍 ##

* NGUI和UGUI的区别
* UGUI的实现属于unity的扩展模块-存储在UnityEngine.UI.dll中（.dll动态链接库dynamic link library）

1)Canvas:

* 对于可视化的GUI，必须是此对象的子对象
* 非可视化GUI，如ToggleGroup等可以不必为此对象的子对象
* 可以相互嵌套使用
* 三种render mode
	* -Screen Space-overlay
	* -Screen Space-camera
	* -Wolrd Space
* Tips：
	* 1.想修改Canvas渲染的透明度 或者 用于检测Canvas下的控件
		* 可以使用**Canvas Group**组件
		* 不能使用Raycast()对Canvas进行检测；应使用GraphicRaycaster来进行检测


2）Rect Transform：

3）常用控件：

* 分为两大类：**visual components** 和 **interaction components**
* visual components:
	* image
	* raw image
	* text
	* mask
* interaction components:
	* button
	* slider
	* toggle
	* scrollbar
	* scroll rect
	* input filed
	* 多数交互组件继承自**Selectable类**
		* 常用属性：
		* Interactive
		* Transition
		* Navigation:对于方向键控制界面ui的选中状态

## 2. 加载场景 ##

* 略