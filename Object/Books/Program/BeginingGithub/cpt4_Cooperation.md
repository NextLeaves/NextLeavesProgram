---

title: cpt 4 Cooperation
date: 3/9/2018 7:54:09 PM 
tags:
- github
- git
categories: git
thumbnail: https://i.imgur.com/G5iATvb.jpg

---

# 第一章 协作 #

* Wrote : 3/9/2018 7:54:31 PM 
* Name  : NextLeaves

* 提交到一个分支
* 从分支创建pull请求
* pull请求合作
* 合并pull请求

---

## 1. 提交到一个分支(branch) ##

* 创建分支
* 选择分支界面
* 提交，在master分支下，只会显示提交到master分支的commits；而分支就会显示分支的commits内容
* 即：提交到分支

### 1.1 在分支中创建pull请求 ###

* 点击**New pull request**按钮，创建pull请求
* base表示需要合并到的分支(master)；compare表示需要合并的分支(自己创建的分支)
* 输入修改意见，然后提交

* 1. 可以对pull请求进行评论
	* 使用**@**符号，选中你想要让其了解的人员
	* 使用emoji可以更好的交流

### 1.2 在对于pull请求的分支再次修改 ###

* 直接划分到分支，进行修改内容
* 然后进行pull request操作
* 在pull request界面可以查看详细内容

### 1.3 测试一个pull请求 ###

* 手动分配克隆的master和分支的内容，进行物理的测试，保证正常的运行

### 1.4 合并pull请求 ###

* 在pull request界面，选择merge pull request即可
* 一般是提交pull的人，不应该merge分支，应该又其他多人确定下，再进行merge操作

### 1.5 pull 请求通知 ###

* 对于被pull request中@到的人员，会自动订阅该pull更新内容，若已经没有兴趣，则可以进行unsubscribe操作

## 2. 问题(issue) ##

* no one is assigned：选择针对问题处理的人员
* no milestone：设置先关的处理时间
* 创建日程表：create milestone
* 可以添加tags，描述issues

### 2.1 提交中引用问题 ###

* 1. 若pull request时，提交的问题和issue有关，则可以使用**#+issue编号**；在**#**前添加前缀，close,fixed,resolve，在合并之后会自动关闭问题

## 3. WIKI ##

* 针对readme内容的增加，对于阅读的方式过于繁杂；通过WIKI的方式，展现终端项目内容，和开发者文档的相关内容

### 3.1 开始使用WIKI ###

* 创建WIKI，使用markdown编辑模式
* create new WIKI 界面，然后再home界面，链接该网址即可

## 4. 创建自己的github博客 ##

* 注意事项：
	* 1. repository的名称一定是：用户名+.github.io；即nextleaves.github.io
	* 2. 可以使用github内置的模版，当然也可以去其他网站寻找模板，也可以自己自定义模板