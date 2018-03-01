#### 1、awk中的动作

在一个模式-动作语句中，模式决定动作什么时候执行，有时候动作会非常简单：一条单独的打印或赋值语句。在有些时候，动作有可能是多条语句，语句之间用换行符或分号分开。

awk的动作中如果有两个或两个以上的语句，需要用分号分隔

动作部分大家理解为花括号里面的内容即可，总体分为：

* 表达式
* 流程控制语句
* 空语句
* 数组（以后如果有时间的话会再写一个awk高级部分进行介绍）

#### 2、awk模式与动作小结

awk命令核心由模式和动作组成

模式就是条件，动作就是具体干什么

1）正则表达式：必须掌握正则，熟练

2）条件表达式：比大小，比较是否相等

3）范围表达式：从哪里来到哪里去

注意BEGIN或END模块只能有一个。BEGIN{}BEGIN{}或者END{}END{}都是错误的。

#### 3、总结awk执行过程

回顾一下awk的结构

awk -F 指定分隔符 ‘BRGIN{}END{}’，如下图

![](/assets/21-18.png)\#awk完整执行过程

```
[root@oldboy ~]# awk -F ":" 'BEGIN{RS="/";print "hello world!"}{print NR,$0}END{print "end of file"}' /server/files/awkfile.txt 
hello world!
1 root:x:0:0:root:
2 root:
3 bin
4 bash
bin:x:1:1:bin:
5 bin:
6 sbin
7 nologin
daemon:x:2:2:daemon:
8 sbin:
9 sbin
10 nologin
adm:x:3:4:adm:
11 var
12 adm:
13 sbin
14 nologin
lp:x:4:7:lp:
15 var
16 spool
17 lpd:
18 sbin
19 nologin
sync:x:5:0:sync:
20 sbin:
21 bin
22 sync
shutdown:x:6:0:shutdown:
23 sbin:
24 sbin
25 shutdown
halt:x:7:0:halt:
26 sbin:
27 sbin
28 halt
mail:x:8:12:mail:
29 var
30 spool
31 mail:
32 sbin
33 nologin
uucp:x:10:14:uucp:
34 var
35 spool
36 uucp:
37 sbin
38 nologin

end of file
```

说明：

我们·同时再命令行定义了分隔符和在BEGIN模式中定义了RS内置变量，在最后通过END模式输出了结果



