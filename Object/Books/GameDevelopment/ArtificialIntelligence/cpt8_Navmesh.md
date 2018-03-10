---

title: cpt 8 Navmesh
date: 3/9/2018 14:00:00 AM 
tags:
- navigation
- automove
categories: unity3d
thumbnail: https://i.imgur.com/mKLM34Y.jpg

---

# 第八章 导航网格 #

* Wrote : 3/9/2018 14:00:00 AM 
* Name  : NextLeaves

* unity3d中内置的导航网格介绍
* 导航网格的使用方法

---

## 1. 简介 ##

* 人工智能寻路需要特定的格式来表示场景
* unity内置的导航网格可以方便的生成navmesh，便于开发者使用

## 2. 设置地图 ##

* 提前给出地图的设计展示图，并说明意图

* 使用导航网格的思路：
	* 1. navigation static设置
	* 2. bake导航网格
	* 3. 为寻路对象添加nav mesh agent组件
	* 4. 使用脚本控制对象，能够移动到鼠标点击的位置

`

	private NavMeshAgent[] navAgents;
	
	void Start()
	{
		navAgents = FindObjectsOfType(typeof(NavMeshAgent)) as NavMeshAgent[];
	}
	
* 知识点：
	* NavMeshAgent组件
	* Camera类的main下的方法ScreenPointToRay函数
	* Input类-mousePosition属性
	* Ray类，RaycastHIt类

### 2.1 针对斜坡的导航 ###

* 修改Slope参数值，达到能够达到自己场景中所设置的目标高度，此可以让对象达到合适的位置
* 如果斜坡和平面无法正确的连接，则可以使用**Off Mesh Links**组件，达到链接的效果

### 2.2 NavMeshLayers的作用 ###

* Edit-ProjectSetting-NavmeshLayers 添加自动寻路的标签
* 设置对象的寻路属性的方法：
	* 选中需要修改导航网格的对象
	* 打开Navmesh界面，Object菜单栏下修改其Walkable属性

### 2.3 Off Mesh Links使用方法 ###

* 可以unity3d中**自动生成**，当然也可以**手动生成**
* 使用**自动生成**方法步骤：
	* 1. 设置对象的static参数值-off mesh links static
	* 2. bake中，可以设置jump distance值，控制跳跃的位置
* 使用**手动生成**方法步骤：
	* 1. 为场景创建**起点**和**终点**的对象
	* 2. 为创建的对象添加组件-**off mesh link**组件

## 3. 本章小结 ##

* 如何生成导航网格？
* 针对于斜坡的网格方式？
* 如何区别使用网格layer？
* 如何链接断裂的网格？
	* 手动
	* 自动
