#### 1、常用快捷键

ctrl + c   取消当前操作     

ctrl + l   清屏 clear 

ctrl + d   退出当前用户

esc  + .   使用上一个命令的最后一个东西

#### 2、移动光标

把光标移动到行&lt;尾&gt;                ctrl + e

把光标移动到行&lt;首&gt;                ctrl + a

把光标向右移动一个单词            ctrl + →

把光标向左移动一个单词            ctrl + ←     

#### 3、剪切（删除）粘贴

把光标所在位置到行首的内容 剪切   ctrl + u

粘贴                            ctrl + y 

把光标所在位置到行尾的内容 剪切   ctrl + k

#### 4、常见的巨坑 

锁屏                                   ctrl + s 

解锁                                   ctrl + q	

##### 注意：

\#命令行输入oldboyedu

\#然后让光标移动到行首 加上注释符号和I am studying

\#然后让光标移动到行尾，加上 linux.site:www.oldboyedu.com;

\#剪切，这一行内容。

\#粘贴3次。

\[root@oldboyedu42-lnb ~\]\# \#找出我用过的命令 -F

\[root@oldboyedu42-lnb ~\]\# \#ctrl + r 

\[root@oldboyedu42-lnb ~\]\# awk -F"\[, \]"   '{pr int $3","$NF}' /oldboy/oldboy.txt

oldboy,31333741

,hello

#### 5、请写出下面linux命令行快捷键的功能？

http://lidao.blog.51cto.com/3388056/1914569

