---

title: cpt 6 Contact With Web
date: 3/11/2018 4:34:56 PM 
tags:
- 2d
- mobile
categories: unity3d
thumbnail: https://i.imgur.com/vQadlzE.jpg

---

# 第六章 与Web服务器的交互 #

* Wrote : 3/11/2018 4:34:57 PM 
* Name  : NextLeaves

* Web服务器简介

---

## 1. Web服务器简介 ##

* **弱联网**的概念：不需要连续在线的游戏，只是提供部分上传和部分下载的网络通信操作
* Unity的**WWW类**提供的HTTP数据通信功能与Web服务器进行数据通信操作
* **HTTP协议**也称为超文本协议传输，是目前应用最广泛的一种网络通讯协议，所有Web服务器的通讯都必须遵循这个协议。最初只是用来定义如何接收、发布HTML页面。
* Web服务器是指遵循HTTP协议的服务器端，通常会采用IIS（仅支持Windows）、Apache、Nginx等服务器软件，这些服务器软件同时支持多种脚本语言进行编程，实现具体的逻辑功能。
* 比较流行的Web服务器脚本语言包括以下4种：
	* ·Asp.Net平台：它是微软的Web框架，支持C#、Basic等语言。一般只适合运行在Windows的IIS上面。
	* ·JSP：采用Java语言的Web开发平台。
	* ·PHP：专门的Web脚本语言。
	* ·Python：也是一种流行的脚本语言，使用Python开发Web服务器通常需要使用一些框架，如Django等。