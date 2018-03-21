---

title: cpt 7 Input And Control
date: 3/21/2018 2:00:00 AM 
tags:
- input
- control
categories: unity3d
thumbnail: 

---

# 第二章 输入与控制 #

* Wrote : 3/21/2018 2:00:00 AM 
* Name  : NextLeaves

* 键盘事件
* 鼠标事件
* 自定义按键事件
* 模型与动画
* GL图像库
* 游戏实例-控制人物移动
* 本章小结

---

## 1. 键盘事件 ##

1. Input.GetKeyDown()
2. Input.GetKeyUp()
3. INput.GetKey()
4. Input.anyKeyDown()
5. Input.anyKey()

## 2. 鼠标事件 ##

1. Input.GetMouseButtonDown()
2. Input.GetMouseButtonUp()
3. Input.GetMouseButton()
4. Input.mousePosition
4. 0:鼠标左键；1:鼠标右键；2:鼠标中键

## 3. 自定义按键事件 ##

1. 自定义按键以轴为判断依据
2. Input.GetAxis("test")
3. Input.GetMousexxx("test")

## 4. 模型与动画 ##

1. 播放动画
	* obj.Getcomponent<Animation>().Play("");
2. 动画剪辑
	* obj.Getcomponent<Animation>().AddClip("")