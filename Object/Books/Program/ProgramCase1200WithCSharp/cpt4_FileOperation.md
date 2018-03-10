---

title: cpt 4 File Operation
date: 3/9/2018 11:24:25 PM 
tags:
- tips
- csharp
categories: program
thumbnail: https://i.imgur.com/gmyFBqq.jpg

---

# 第四章 文件操作 #

* Wrote : 3/9/2018 11:25:36 PM 
* Name  : NextLeaves

* 1. 文件基本操作
* 2. 文件夹基本操作
* 3. 文件流操作
* 4. 加密、解密及解压文件

---

## 1. 文件基本操作 ##

### 1.1 获取文件信息 ###

1) 获取文件长度：

* 名称空间：System.IO;
* File类的Open()
* FileStream类的Length值
* OpenFileDialog类：用于打开选择window文件

2）获取文件扩展名：

* 利用Substring方法进行获取扩展名
* LastIndexOf()

3）获取文件创建时间

* FileInfo
* CreationTime()

4）文件上一次修改时间

* FileInfo
* LastWriteTime

5）获取路径无效字符

* Path
* GetInvalidPathChars()

6）创建文件、删除文件

* File
* Creat()
* Delete()

7）设置随机的文件名，文件夹名

* Guid
* NewGuid()

8）建立临时文件

* Path
* GetTempFilePath():创建一个0字节的临时文件，用于临时保存
* AppendText()
* FileInfo
* StreamWriter

9）根据日期动态建立文件

* DateTime
* Now属性
* File
* Create()

10）清空回收站的所有文件

* Directory


## 2. 文件夹基本操作 ##

## 3. 文件流操作 ##

## 4. 加密、解密及解压文件 ##
