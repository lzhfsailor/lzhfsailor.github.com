---
layout: post
title:  "WEB前端开发学习第一天：notpad plus plus + emmet高效率开发环境搭建"
date:   2014-04-30 15:45:15
categories: web
description: WEB前端开发学习第一天：介绍notpad++及其插件emmet高效率开发环境搭建，emmet安装使用过程中碰到的问题

---
# 环境搭建 #
1. 下载Emmet和Python Script
2. 安装：插件可以用notpad++自身携带的插件管理器安装，通过 Notepad++ 中的 Plug Manager，直接在「插件」-「Plug Manager」-「Show Plug Manager」中找到 Emmet，勾选后点击 Install 便可安装。也可以下载dll文件复制到notpad++插件目录中
3. emmet还支持sublime text，Dreamweaver，Eclipse/Aptana等常见编辑器及IDE
4. 备注：几乎所有的关于安装Emmet的文档中都没有提到需要安装Python Script，具体原因未知。在我的win7 32位系统上，不安装Python Script插件不可用


参考[emmet官方网站](http://docs.emmet.io/ "emmet")


----------
# Emmet使用简介 #
- Emmet会自动把doctype补全
	- html:5 或者 ! 生成 HTML5 结构
	- html:xt 生成 HTML4 过渡型
	- html:4s 生成 HTML4 严格型
- DIV及列表自动生成
	- #page>div.logo+ul#navigation>li*5>a{Item $}
- 具体动态图如下
	> ![html5](pic\emmet.gif)

--------------
# 碰到的问题 #

- Emmet需要 Python Script 的支持，因此这两款插件必须同时安装才能使用。开始只安装了Emmet，导致快捷键及菜单中选择自动完成没有反应。
- Emmet插件装好后，使用快捷键没反应，而从菜单里选择可以使用。原因是自动完成的快捷键与其余插件或者notpad++本身快捷键冲突。解决方法是修改快捷键。