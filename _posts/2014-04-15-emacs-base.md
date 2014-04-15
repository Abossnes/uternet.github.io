---
layout: post
title: Emacs 基本操作
date: 2014-04-15
---

窗口操作：

C-x 1           关闭除本窗口外的所有窗口（缓冲区并未关闭）  
C-x 2           水平分割窗口  
C-x 3           垂直分割窗口  
C-x o		切换窗口  

缓冲区操作：

C-x b           切换缓冲区  
C-x k           关闭缓冲区  

文件操作：

C-x C-f         打开或新建文件  
C-x C-s         保存文件  
C-x C-w		文件另存为  
C-x C-v		打开新文件，并关闭当前缓冲区  

移动光标：

M->             移动到文件末尾（事实上是M-S-> 因为>是上档键，必需先按Shift）  
M-<             移动到文件开头（同上）  
C-n             移动到下一行  
C-p             移动到上一行  
C-a             移动到行头  
C-e             移动到行尾   
M-m             移动到行头非空白处  
M-j		回车，并在下一行产生适当的缩进  

移屏：

C-v		下移一屏  
M-v		上移一屏  
C-l		重绘屏幕，将当前行置于窗口中部，重复按则交替显示在窗口上部和下部  

搜索：

C-s		向前搜索   
C-r		后退搜索   

标记文本：

C-x h		全选   
C-@		设定标记起始点(@位于上档键，所以需要Shift配合)   
M-w		复制标记的文本   
C-w		剪切标记的文本   
C-y		粘贴文本   

运行SHELL命令：

M-! command	打开一个名为*Shell Command Output*的窗口显示运行结果   
M-x shell	运行一个子shell   
M-x term	运行一个子shell,这是一个完整的shell模拟   
M-x eshell	运行eshell,这是一个由elisp写成的shell    


