### 一、范围模式

![](/assets/21-17.png)

* 范围模式简单理解就是从哪里来，到哪里去。

* 匹配从条件1开始到条件2介绍的范围

**1）**还记得sed使用地址范围来处理文本内容嘛？awk的范围模式，与sed类似，但是又有不同，awk不能直接使用行号来作为范围起始地址，因为awk具有内置变量NR来存储记录号，所有需要使用NR=1,NR=5这样来使用。

**2）**范围模式处理的原则是：先匹配从第一个模式的首次出现到第二个模式的首次出现之间的内容，执行action。然后匹配从第一个模式的下一次出现到第二个模式的下一次出现，直到文本结束。如果匹配到第一个模式而没有匹配到第二个模式，则awk处理从第一个模式开始直到文本结束全部的行。如果第一个模式不匹配，就算第二个模式匹配，awk依旧不处理任何行。

```
awk '/start pos/,/end pos/{print $)} passwd oldboy'
awk '/start pos/,NR==XXX{print $0}' passwd oldboy
```

范围模式的时候，范围条件的时候，表达式必须能匹配一行。

#### 例一：

```
[root@www files]# awk 'NR==2,NR==5{print NR,$0}' count.txt 
2 bin x bin bin sbin nologin
3 daemon x daemon sbin sbin nologin
4 adm x adm var adm sbin nologin
5 lp x lp var spool lpd sbin nologin
```

说明：

条件是：从第二行，到第五行

动作是：显示行号（NR）和整行（$0）

合起来就是显示第二行到第五行的行好和整行的内容

#### 例二：

```
[root@www files]# awk '/^bin/,NR==5{print NR,$0}' awkfile.txt 
2 bin:x:1:1:bin:/bin:/sbin/nologin
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
4 adm:x:3:4:adm:/var/adm:/sbin/nologin
5 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

说明：

条件是：从以bin开头的行，到第五行

动作是：显示行号和整行内容

合起来就是显示从以bin开头的行，到第五行中的行号和整行内容。

例三：

```
[root@www files]# awk -F":" '$5~/^bin/,/^lp/{print NR,$0}' awkfile.txt
2 bin:x:1:1:bin:/bin:/sbin/nologin
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
4 adm:x:3:4:adm:/var/adm:/sbin/nologin
5 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

说明：

条件：从第五列以bin开头的行到以lp开头的行

动作：显示行号和正航内容

合起来：从第三列以bin开始的行到以lp开头的行并显示其行号和整行内容

```
[root@www files]# awk -F: '$5~/^bin/,$5~/^lp/{print NR,$0}' awkfile.txt 
2 bin:x:1:1:bin:/bin:/sbin/nologin
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
4 adm:x:3:4:adm:/var/adm:/sbin/nologin
5 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

说明：

条件：从第三列以bin开头字符串的行到第三列以lp开头字符串的行

动作：显示行号和整行

#### 练习题：

1、简单叙述什么是范围模式？

2、显示第二行到第五行的行及整行的内容

3、第三列以bin开始的行到以lp开头的行并显示其行号和整行内容

