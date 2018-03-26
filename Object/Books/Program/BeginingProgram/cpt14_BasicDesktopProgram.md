---

title: cpt 14 Basic Desktop Program
date: 3/21/2018 10:19:51 PM 
tags:
- begining
- csharp
categories: program
thumbnail: https://i.imgur.com/XBiiMqE.jpg

---

# 第十四章  #

* Wrote : 3/21/2018 10:19:52 PM 
* Name  : NextLeaves

* 如何使用wpf设计器
* 如何使用label、textblock等控件向用户呈现效果
* 如何使用button等控件触发事件
* 如何使用textbox控件，让用户输入
* 如何使用···

---

## 1. 基本桌面编程 ##

* GUI（Graphical User Interface）
* silverlight:创建交互式web应用程序

## 2. XMAL ##

1. 使用DirectX的高级功能：
	* 浮点坐标和矢量图形
	* 高级2D和3D渲染功能
	* 高级字体处理和渲染
	* UI对象支持纯色、渐变和纹理填充，并可选择透明度
	* 可在任何情形中使用的动画分镜头设计，包括鼠标单击按钮等用户触发事件
	* 可使用可重用的资源来动态设置控件的样式

2. 关注点分离
	* “代码隐藏文件”功能
	* Blend for Visual Studio是设计师们为WPF制作GUI时的首选工具 
* XMAL基础知识
	* 闭合标签
	* 属性在前标签内
	* content可以在前后标签之内
	* **名称空间：**
		* URL/URI
		* xmlns:x="" ； 可以不再后面的控件中添加前缀
	* **代码隐藏文件：**

## 14.2 动手实践 ##	

* WYSIWHG(所见即所得)

---

1. **WPF控件**
	* GUI和代码文件的打包体
	* 属性和依赖属性(dependency property)
	* 触发事件
		* button：click
		* listbox：selectionchanged