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
	* sprite animation
	* sprite autofly
	* control player
	* instance enemy
	* act between player and enemy 

---

## Preface ##

1. Unity4.3 引入2D开发模式
2. 学习流程：
	* sprite editor
	* sprite animation
	* physics 2d
	* script in 2d game

## 1.构建初始场景 ##

### 1.1 创建场景 ###

1. 2D工程和3D工程在初创的区别：
	* scene界面的2d是否开启
	* main camera的projection
	* 添加素材，默认为sprite/texture
	* Editor Setting - Default behavior mode
2. 统一文件格式-
	1. _Scenes
	2. _Scripts
	3. ---
3. 灯光效果，让场景变得和谐

### 1.2 添加场景元素 ###

1. sprite中, Background、Foreground、Sorting Layer、Order in Layer
2. sprite - texture type - sprite(2d and ui)
	1. piexlstounits means 多少个像素点等于unity中的单元格
3. 一般的绘制顺序：Default - Background - Character - Foreground - UI
4. 经验：
	1. 一般若需要放大图片，可以通过调整scale值，进行强制的缩小和放大；但会导致图片模糊、锯齿增加；在图片像素足够大的前提下，可以通过更改piexlstounits值，越小所释放出的像素点越多，画质却不改变
	2. Camera的Size属性：决定摄像机所容纳的范围

## 2.Swan's Animation ##

### 2.1 生成多个飞行姿态 ###

1. sprite mode ：multiple，亦可切割单张sprite
2. sprite editor - slice ：可自动、可手动，进行自己合适的切割方式。提示：必须点apply才能生效

### 2.2 创建动画 ###

1. Animation window - 可以进行sprite的操作
2. samples值：决定对动画的采样速率，即值越大，动画切换速度越快；反之，越慢
3. Rigidbody - Gravity Scale = 0 means 无重力

### 2.3 swan 随机飞动 ###

1. 属性、字段：
	* Rigidbody
	* edge from four sides
	* min/max speed
2. 方法：
	* 随机种子-由当时时间决定
	* 使用协程，同时在携程函数中再次调用StartCorutine，实现循环操作（可以理解无法终止的递归）
	* localscale.x*=-1 ，实现sprite的翻转
	* 并最后销毁操作

## 3. 创建Mr.Bean 动画 ##

1. 创建空对象、设置相关参数，如：sorting layer，order in layer, layout , tag
2. 创建AC
	* jump
	* speed
	* die
	* run
	* shoot（新层次中创建）

## 4. 2d碰撞功能 ##

1. box 2dcollider ， circle 2dcollider
2. edge collider2d限制圈内物体不能出去，而box，cicle会挤出内部的具有碰撞体的物体

## 5. 游戏控制 ##

### 5.1 主角运动控制 ###

1. 属性、字段
	* moveForce
	* jumpForce
	* maxSpeed
	* groundCheck
	* grounded
	* anim
2. 方法：
	* Physics2D.Linecast()检测是否有主角是否在地面
		* 层掩码(bitmask)，（序列掩码）layer index
		* 前者为，函数所需要；后者为编辑器中Layer中的序列号，可通过移位操作(1<<layer index)，可得到bitmask；或者使用LayerMask.Getmask()
	* Flip()：实现角色翻转的效果
	* FixedUpdate()：执行相关的函数
		* 移动，通过rb.AddForce()
		* 执行动画，anim.SetTrigger()
		* 跳跃，类似

### 5.2 主角的射击控制 ###

1. 属性，字段
	* rocket
	* speed
	* anim
	* playControl：获取是否在地面的效果
2. 方法：
	* 对应的调用Instantiate

### 5.3 主角与敌人的交互 ###

1. 随机生成敌人（在合适的位置，调用生成即可）
2. InvokeRepeating()实现重复调用
3. Rhysics2D.OverlapPointAll()，返回重叠的所有对象
4. 实现触发操作的
	1. void OnCollisionEnter2D(Collision2D others)
	2. void OnTriggerEnter2D(Collider2D others)