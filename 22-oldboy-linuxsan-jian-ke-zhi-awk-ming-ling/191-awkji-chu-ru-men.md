要弄懂awk程序，必须熟悉了解这个工具的规则。本实战笔记的目的是通过实际案例或面试题带同学们熟练掌握awk在企业中的用法，而不是awk程序的帮助手册。

#### 1、 awk简介

* 一种名字怪异的语言
* 模式扫描和处理

awk不仅仅时linux系统中的一个命令，而且是一种编程语言，可以用来处理数据和生成报告（excel）。处理的数据可以是一个或多个文件，可以是来自标准输入，也可以通过管道获取标准输入，awk可以在命令行上直接编辑命令进行操作，也可以编写成awk程序来进行更为复杂的运用。本章主要讲解awk命令的运用。

#### 2、学完awk你可以掌握：

1）记录与字段

2）模式匹配：模式与动作

3）基本的awk执行过程

4）awk常用内置变量（预定义变量）

5）awk数组（工作常用）

6）awk语法：循环，条件

7）awk常用函数

8）向awk传递参数

9）awk引用shell变量

10）awk小程序及调试思路

#### 3、awk环境简介

    [root@oldboy ~]# cat /etc/redhat-release 
    CentOS release 6.8 (Final)
    [root@oldboy ~]# uname -r
    2.6.32-642.el6.x86_64
    [root@oldboy ~]# ll `which awk`
    lrwxrwxrwx. 1 root root 4 Dec 23 20:25 /bin/awk -> gawk
    [root@oldboy ~]# awk --version
    GNU Awk 3.1.7
    Copyright (C) 1989, 1991-2009 Free Software Foundation.

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program. If not, see http://www.gnu.org/licenses/.

#### 4、awk的格式

* awk指令是由模式，动作，或者模式和动作的组合组成。

* 模式既pattern,可以类似理解成sed的模式匹配，可以由表达式组成，也可以是两个正斜杠之间的正则表达式。比如NR==1，这就是模式，可以把他理解为一个条件。
* 动作即action，是由在大括号里面的一条或多条语句组成，语句之间使用分号隔开。比如awk使用格式：

![](/assets/21-2.png)

awk处理的内容可以来自标准输入（&lt;），一个或多个文本文件或管道。

![](/assets/21-9.png)

* pattern既模式，也可以理解为条件，也叫找谁，你找谁？高矮，胖瘦，男女？都是条件，既模式。

* action既动作，可以理解为干啥，找到人之后你要做什么。模式和动作的详细介绍我们放在后面部分，现在大家先对awk结构有一个了解。



