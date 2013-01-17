---
layout: post
title: C#下OpenGL的配置实用
description: C#下OpenGL的配置实用,VS2010
categories: Tech
tags: Tech C# OpenGL
---

##C#下OpenGL的配置实用
1. 安装VS2010，下载csgl.1.4.1.dll文件
2. 双击csgl.1.4.1.dll \ libinstall內的install.bat安装
3. 在VS2010中新建一个C#的windows窗体程序
4. 右击项目或者项目中的“引用”，添加引用，浏览至lib文件夹中的csgl.dll文件
5. 写一个类：
+ 右击你的项目，添加--->类，命名为MyOpenGL，名字随便。
+ 在类中写入以下画图程序代码
> `using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using CsGL.OpenGL;    
namespace WindowsFormsApplication2{  
    class MyOpenGL : OpenGLControl{  
        public override void glDraw(){  
            GL.glClear(GL.GL_COLOR_BUFFER_BIT | GL.GL_DEPTH_BUFFER_BIT); 
            GL.glBegin(GL.GL_POINTS);
            GL.glVertex2i(100, 50);
            GL.glVertex2i(100, 130);
            GL.glVertex2i(150, 130);
            GL.glEnd();
            GL.glFlush();
        }  
        protected override void InitGLContext(){  
            GL.glClearColor(1.0f, 1.0f, 1.0f, 0.0f);  
            GL.glColor3f(0.0f, 0.0f, 0.0f);  
            GL.glPointSize(4.0f);}  
        protected override void OnSizeChanged(EventArgs e){  
            base.OnSizeChanged(e);
            GL.glMatrixMode(GL.GL_PROJECTION);
            GL.glLoadIdentity();
            GL.gluOrtho2D(0.0, Size.Width, 0.0, Size.Height);}}}
`

6. 在Form1.cs中加入代码，调用类：
+ 右击Form1.cs，选择查看代码
+ 添加代码如下：
> ` public Form1(){  
            Text = "My First OpenGL!";  
            view.Dock = DockStyle.Fill;  
            Controls.Add(view);  
            InitializeComponent();}  
        MypenGL opGL = new MypenGL();`

