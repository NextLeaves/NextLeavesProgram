---

title: cpt 3 2D space shooter
date: 2/14/2018 4:15:55 PM 
tags:
- unity3d
- 2d
categories: unity3d
thumbnail: https://i.imgur.com/tTWr7zA.jpg

---

# 第三章 星际迷航 #

* Wrote : 2/14/2018 4:15:55 PM 
* Name  : NextLeaves

* 2D游戏中所需要的技术：
	* 键盘控制飞船的移动
	* 发射子弹射击目标
	* 随机生成大量的障碍物（aerolite）	
	* 计分
	* 实现游戏对象的生命周期

---

## 1. 导入资源、贴图、材质 ##

* Asset Store中有Space shooter资源包
* 设置Camera的相关参数：
	* 达到2D游戏的效果内容
	* 并设置整个游戏界面的**width**和**height**的值400 * 600

### 1.1 创建飞船对象 ###

* Rigidbody组件为物理系统的必备组件、也是基础组件，**否则无法生效物理系统**
* 设置飞船的相关特效内容
* 设置飞船组件的相关参数
	* Collider：isTrigger
	* Rigidbody：！useGravity

### 1.2 添加图片背景 ###

* 利用Quad游戏对象，添加对应的背景图
	* 设置Texture Type为default
	* **shader**为Unlit/Texture
* 调整位置，并达到良好的效果，编写移动脚本，达到背景图移动的效果
	* 1）利用offset值进行移动；前提背景图需要形成环形图片，既重合时没有太多生硬感
	* 2）暂不清楚，但是基础理解为使用Mathf.Repeat()，利用重复移动方式

## 2. 编写脚本代码 ##

### 2.1 键盘控制飞船移动 ###

* Rigidbody.velocity
* mathf.Clamp()，限制飞船移动范围（直接限制飞船的tranform.postion）
	* 此时，可以利用枚举实现对范围的控制
* 旋转飞船，使左右移动的时候更加和谐，使用**速度和倾斜角度**来实现飞船旋转

### 2.2 实现射击行为 ###

* 组件Rigidbody和Collider一般在空的父物体上
* 特效一般在子对象上
	* 无法加载子弹
	* 子弹不消失，消耗资源
* 脚本控制子弹的发射
	* 设计子弹的发射位置，一般在飞机对象上添加空对象
	* 发射频率，利用Time.time方法
* 管理生成物体的生命周期
	* 为了减少资源的消耗，达到一个较低的水平
	* 1）使用IEnumertor效果，延迟消失
	* 2）使用Destroy(obj,time)，双参数来延迟销毁函数

### 2.3 添加小行星 ###

* 逻辑思考：
	* 随机产生小行星
	* 击中小行星，小行星消失
	* 飞船碰到小行星，消失
* 所用到函数：
	* Random.InsideUnitSphere
	* angleVelocity
	* tumple:float
* 逻辑顺序：
	* 创建小行星对象
	* 控制随机旋转的函数，让陨石更加生动
	* 控制设计小行星的功能
	* 添加小行星运动的功能
	* 添加小行星随机产生的逻辑
	* 添加小行星批量产生的功能

## 3. 收尾部分 ##

### 3.1 碰撞的爆炸声音 ###

* 使用对应的AudioSource即可

### 3.2 飞船射击音频 ###

* 同上

### 3.3 背景音乐 ###

* 同上

### 3.4 添加计分文本 ###

* 利用Canvas达到效果
* 当前分数score
* 最大分数maxScore

### 3.5 重开游戏 ###

* GameController脚本控制
* 使用flag方式