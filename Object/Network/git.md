---

title: git
date: 3/19/2018 6:32:26 PM  
tags:
- git
- coorperation
categories: git
thumbnail: https://i.imgur.com/HrTZ1Fv.jpg

---

# 第一章 Git #

* Wrote : 3/19/2018 6:36:26 PM  
* Name  : NextLeaves

* Git入门基础

---

## 1. Git入门基础 ##

* git init
* git config [option]
	* git config --global user.email xxx
	* git config --global user.name xxx
* git add [option]
	* git add .
	* git add xxx.txt
* git commit [option]
	* git commit -m "xxx"
	* git commit -am "xxx"
* git status
* git diff xxx.txt

## 2. 时光机穿梭 ##

1. **版本回退**
	* git log
		* git log --pretty=oneline
		* commit id
	* git reset --hard HEAD^
	* git reset --hard HEAD^^
	* git reset --hard HEAD~100
	* git reflog
	* [Warning]**--hard**参数的使用，必须使用！
2. **工作区和暂存区**
3. **管理修改**
	* git diff HEAD -- xxx.txt
*  **撤销修改**
	*  git checkout -- xxx.txt
	*  git reset HEAD xxx.txt
*  **删除文件**
	*  git rm xxx.txt  
	*  git checkout HEAD -- xxx.txt / git checkout HEAD xxx.txt
	*  rm xxx.txt
	*  git checkout -- xxx.txt

## 3. 远程仓库 ##

1. ssh-keygen -t rsa -C "your email address"
2. **添加远程库**
	* git remote add origin xxx
	* git push -u origin master
	* git push origin master
	* git clone xxx

## 4. 分支管理 ##

1. **创建与合并分支**
	* git branch dev , git checkout dev ; / git checkout -b dev
	* git checkout dev
	* git checkout master , git merge dev
	* git branch -d dev

2. 解决冲突
	* git merge dev
	2. 失败之后修改不同文件内容达到相同，即可再次提交
	3. git log --graph --pretty=oneline --abbrev-commit

3. 分支管理策略
	* git merge --no--ff -m "abort fast forward pattern" dev
	2. git log --graph --pretty=oneline --abbrev-commit

4. Bug分支
	* git stash
	* 将要修复master的issue-101
		* git checkout master
		* git branch -b issue-101
		* git commit -am "fix issue-101"
		* git checkout master
		* git merge issue-101
		* git branch -d issue-101
	* git stash list
		* git stash apply xxx
		* git stash drop xxx
		* git stash pop xxx

* Feature分支
	* 未合并的分支，但需要删除分支; git branch -D feature-01

* 多人协作
	* git push origin master
	* git push origin dev
	* 解决协作中冲突：
		* git pull
		* git branch --set-upstream dev origin/dev
		* git pull

## 4. 标签管理 ##

1. **创建标签**
	* git tag v1.0
	* git tag v0.9 commitId
	* git tag
	* git show v0.9
	* git tag -a v0.1 -m "version 0.1 released" commitId
	* git tag -s v0.2 -m "signed version 0.2 released" commitId
* **操作标签**
	* git tag -d v0.1
	* git push origin v1.0
	* git push origin --tags
	* 远程删除tag
		* git tag -d v1.0
		* git push origin :refs/tags/v1.0

## 5. 使用Github/码云 ##

* git push origin master 
* git push gitee master

## 6. 自定义Git ##

1. **忽略特殊文件**
	* .gitignore
	* git add -f fileName
		
`

	# Python:
	*.py[cod]
	*.so
	*.egg
	*.egg-info
	dist
	build

	# Windows:
	Thumbs.db
	ehthumbs.db
	Desktop.ini
	
	# Python:
	*.py[cod]
	*.so
	*.egg
	*.egg-info
	dist
	build
	
	# My configurations:
	db.ini
	deploy_key_rsa

2. **配置别名**
	* git config --global alias.st status
	* git config --global alias.unstage 'reset HEAD'

3. **搭建Git服务器**
	* 