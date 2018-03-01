### 一、linux快捷键

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

[http://lidao.blog.51cto.com/3388056/1914569](http://lidao.blog.51cto.com/3388056/1914569)

### 二、vi、vim快捷键

#### 1、移动光标与编辑

![](/assets/36-1.png)

#### 2、把光标移动到行尾

$

#### 3、把光标移动到开头

0   ^

#### 4、把光标移动到文件的结尾

G    :$

    [root@oldboyedu45-lnb ~]# sed -n '10p' vim.txt 
    # Updated from RFC 1700, ``Assigned Numbers'' (October 1994).  Not all ports
    [root@oldboyedu45-lnb ~]# sed -n '$p' vim.txt 
    DNS2=223.6.6.6

#### 5、把光标移动到文件的开头

gg   :1

#### 6、把光标移动到文件第100行

100gg   :100

#### 7、把光标移动到行尾并进入编辑模式

A

#### 8、在当前行下面追加一个空行并进入编辑模式

o \(小写字母o\)

#### 9、在当前行上面插入一个空行并进入编辑模式

O\(大写字母O\)

#### 10、删除光标所在位置到行尾的内容并进入编辑模式

C

#### 11、删除光标所在位置到行尾的内容

D

#### 12、删除当前行

dd

#### 13、删除光标所在行到文件最后一行内容

dG

#### 14、复制当前行

yy

#### 15、粘贴

p

#### 16、粘贴

100p

#### 17、撤销上一次的操作

u

#### 18、恢复上一次的操作

ctrl + r

#### 19、删除光标所在位置的1个字符

x

#### 20、批量操作-可视块模式  VISUAL BLOCK

##### \#批量的编辑

1）ctrl + v  \#进入可视块模式

2）选择你要批量编辑的部分 位置

3）I\(shift+i\) 编辑

4）编辑完成之后 按esc退出编辑 等待

#### 21、其他

/你要搜索的内容    默认向下搜索

继续向下搜索n 

 继续向下搜索N 

?你要搜索的内容    默认向上搜索

####  22、添加行号 

:set nu

:set nonu

:noh  取消语法高亮

#### 23、help

:help  A

:h     A

:h     :wq

#### 24、把文件中的第1行到10行复制到最后一行后面

:1,100copy$

:1,100co$

#### 25、把文件中的第1行到10行移动到10777后面

:1,100move10777

:1,100mo10777

