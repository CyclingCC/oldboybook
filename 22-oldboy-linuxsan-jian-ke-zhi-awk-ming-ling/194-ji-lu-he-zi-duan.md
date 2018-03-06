接下来我给大家带来两个新概念记录和字段，这里为了方便大家理解可以把记录就当作行即记录==行，字段相当于列，字段==列。

![](/assets/21-12.png)

#### 1、记录（行）

查看一下下面这段文字

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
```

##### 思考：

一共有多少行呢？你如何知道的？通过什么标志？

awk对每个要处理的输入数据认为都是具有格式和结构的，而不仅仅是一堆字符串。默认情况下，每一行内容都是一条记录，并以换行符分隔（\n）结束

#### 2、记录分隔符-RS

#### ![](/assets/21-4.png)

* awk默认情况下每一行都是一个记录（record）

* RS既record separator输入输出数据记录分隔符，每一行是怎么没的，表示每个记录输入的时候的分隔符，既行与行之间如何分隔。

* NR既number of record 记录（行）号，表示当前正在处理的记录（行）的号码。

* ORS既output record separator 输出记录分隔符。

awk使用内置变量RS来存放输入记录分隔符，RS表示的是输入的记录分隔符，这个值可以通过BEGIN模块重新定义修改

1）使用“/”为默认记录分隔符

示例文件：

```
[root@oldboy ~]# cat /server/files/awkfile.txt 
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
```

```
[root@oldboy ~]# awk 'BEGIN{RS="/"}{print NR,$0}' /server/files/awkfile.txt 
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
```

命令说明：

在每行的开始先打印输出NR（记录号行号），并打印出每一行$0（整行）的内容。

我们设置RS（记录分隔符）的值为“／”，表示一行（记录）以“／”结束

在awk眼中，文件是从头到尾一段连续的字符串，恰巧中间有些\n（回车换行符），\n也是字符哦。

##### 我们回顾下“行（记录）”到底是什么意思？

* 行（记录）：默认以\n（回车换行）结束。而这个行的结束不就是记录分隔符嘛。
* 所以在awk中，RS（记录分隔符）变量表示着行的结束符号（默认是回车换行）

##### 在工作中，我们可以通过修改RS变量的值来决定行的结束标志，最终来决定“每行”的内容。

##### 为了方便人们理解，awk默认就把RS的值设置为“\n”

注意：

awk的BEGIN模块，我会在后面（模式-BEGIN模块）详细讲解，此处大家仅需要知道在BEGIN模块里面我们来定义一些awk内置变量即可。

#### 3、对$0的认识

* 如2、的例子，可以看出awk中$0表示整行，其实awk使用$0来表示整条记录。记录分隔符存在RS变量中，或者说每个记录以RS内置变量结束。

* 另外，awk对每一行的记录号都有一个内置变量NR来保存，每处理完一条记录，NR的值就会自动+1

* 下面通过示例来加深印象。

1）NR记录号

```
[root@oldboy ~]# awk '{print NR,$0}' /server/files/awkfile.txt 
1 root:x:0:0:root:/root:/bin/bash
2 bin:x:1:1:bin:/bin:/sbin/nologin
3 daemon:x:2:2:daemon:/sbin:/sbin/nologin
4 adm:x:3:4:adm:/var/adm:/sbin/nologin
5 lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
6 sync:x:5:0:sync:/sbin:/bin/sync
7 shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
8 halt:x:7:0:halt:/sbin:/sbin/halt
9 mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
10 uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
```

命令说明：

NR既number of record，当前记录的记录号，刚开始学也可以理解为行号。

$0表示整行或者说整个记录

#### 4、企业面试题：按单词出现频率降序排序（计算文件中每个单词的重复数量）

注：（此处使用sort与uniq即可）

题目

```
题目创建方法：sed -r '1,10s#[^a-zA-Z]+# #g' /etc/passwd>/server/files/count.txt
```

```
[root@oldboy files]# cat /server/files/count.txt 
root x root root bin bash
bin x bin bin sbin nologin
daemon x daemon sbin sbin nologin
adm x adm var adm sbin nologin
lp x lp var spool lpd sbin nologin
sync x sync sbin bin sync
shutdown x shutdown sbin sbin shutdown
halt x halt sbin sbin halt
mail x mail var spool mail sbin nologin
uucp x uucp var spool uucp sbin nologin
```

思路：

让所有单词排成一列，这样每个单词都是单独的一行

1\)设置RS值为空格

2）将文件里面的所有空格替换为回车换行符“\n”

3\)grep所有连续的字母，grep -o参数让他们排成一列

方法一：

```
[root@oldboy files]# awk 'BEGIN{RS="[ ]+"}{print $0}' count.txt | sort |uniq -c|sort
      1 
      1 bash
      1 lpd
      2 daemon
      2 lp
      3 adm
      3 halt
      3 mail
      3 root
      3 shutdown
      3 spool
      3 sync
      3 uucp
      4 var
      5 bin
      6 nologin
     10 x
     12 sbin
```

方法二：

```
[root@oldboy files]# cat count.txt | tr " " "\n" | sort | uniq -c | sort
      1 bash
      1 lpd
      2 daemon
      2 lp
      3 adm
      3 halt
      3 mail
      3 root
      3 shutdown
      3 spool
      3 sync
      3 uucp
      4 var
      5 bin
      6 nologin
     10 x
     12 sbin
```

方法三：

```
[root@oldboy files]# grep -o "[a-zA-Z]\+" count.txt | sort | uniq -c | sort
      1 bash
      1 lpd
      2 daemon
      2 lp
      3 adm
      3 halt
      3 mail
      3 root
      3 shutdown
      3 spool
      3 sync
      3 uucp
      4 var
      5 bin
      6 nologin
     10 x
     12 sbin
```

#### 5、awk记录知识小结

NR存放着每个记录的号（行号）读取新行时候会自动+1

RS是输入数据的记录的分隔符，简单理解就是可以指定每个记录的结尾标志。

RS作用就是表示一个记录的结束

当我们修改了RS的值，最好配合NR（行）来查看变化，也就是修改了RS的值通过NR查看结果，调试awk程序。

ORS输出数据的记录的分隔符

##### awk学习技巧一则：

大象放冰箱分几步？打开冰箱，把大象放进去，关闭冰箱门。

awk也是一样的，一步一步来，先修改了RS，然后用NR调试，看看到底如何分隔的。然后通过sort排序，uniq -c去重

#### 6 、字段（列） {#字段列}

* 每条记录都是由多个区域（field）组成的，默认情况下区域之间的分隔符是由空格（即空格或制表符）来分隔，并且将分隔符记录在内置变量FS中，每行记录的区域数保存在awk的内置变量NF中。

![](/assets/21-6.png)

* FS既field separator,输入字段（列）分隔符。分隔符就是菜刀，把一行字符串切为很多个区域。

* NF既number of fileds，表示一行中列（字段）的个数，可以理解为菜刀切过一行后，切成了多少份。

**OFS输出字段（列）分隔符**

* awk使用内置变量FS来记录区域分隔符的内容，FS可以在命令行上通过-F参数来更改，也可以通过BEGIN模块来更改。

* 然后通过$n,n是整数，来取被切割后的区域，$1取第一个区域，$2取第二个区域，$NF取最后一个区域。

**下面我们通过示例来加强学习。**

1）指定分隔符

```
[root@oldboy files]# awk -F ":" 'NR>=2&&NR<=5{print $1,$3}' /server/files/awkfile.txt 
bin 1
daemon 2
adm 3
lp 4
```

命令说明：

以：（冒号）为分隔符，显示第2行到第5行之间的第一区域和第三区域。

* 此处的FS知识一个字符，其实它可以指定多个的，此时FS指定的值可以是一个正则表达式。

* 正常情况下，当你指定分隔符（非空格）的时候，例如指定多个区域分隔符，每个分隔符就是一把刀，把左右两边切为两个部分。

**企业面试题：**同时取出chensiqi和215379068这两个内容（指定多分隔符）

```
[root@oldboy files]# echo "I am chensiqi,my qq is 1234567890">>/server/files/chensiqi.txt
[root@oldboy files]# cat /server/files/chensiqi.txt 
I am chensiqi,my qq is 1234567890
```

**思路：**

我们用默认的想法一次使用一把刀，需要配合管道的。如何同时使用两把刀呢？看下面的结果

```
[root@oldboy files]# awk -F "[ ,]" '{print $3,$NF}' /server/files/chensiqi.txt 
chensiqi 1234567890
```

命令说明：

通过命令-F参数指定区域分隔符

\[ ,\]是正则表达式里面的内容，它表示一个整体，“一个”字符，既空格或者逗号（,），合并在一起，-F “\[ ,\]”就表示以空格或者逗号（,）为区域分隔符

##### 小技巧：

在动作（‘{print $3,$NF}’）里面的逗号，表示空格，其实动作中的逗号就是OFS的值，我们会在后面说明。刚开始大家把动作中的都逗号，当作空格即可。

2）默认分隔符和指定分隔符会有些差异

```
[root@oldboy files]# ifconfig eth0 | awk 'NR==2' >/server/files/awkblank.txt
[root@oldboy files]# cat /server/files/awkblank.txt 
          inet addr:192.168.197.133  Bcast:192.168.197.255  Mask:255.255.255.0
```

\#默认分隔符时候

```
[root@oldboy files]# awk '{print $1}' /server/files/awkblank.txt 
inet
```

\#指定分隔符时候

```
[root@oldboy files]# awk -F "[ :]+" '{print $1}' /server/files/awkblank.txt 
[root@oldboy files]# awk -F "[ :]+" '{print $2}' /server/files/awkblank.txt 
inet
```

命令说明：

awk默认的FS分隔符对于空格序列，一个空格或多个空格tab都认为是一样的，一个整体。

这个文件的开头有很多连续的空格，然后才是inet这个字符

当我们使用默认的分隔符的时候，$1是有内容的。

当我们指定其他分隔符（非空格）时候，区域会有所变化

到底为何会这样，我们在这里不再深入研究，只要了解有这种情况，注意一下即可。

#### 7、ORS与OFS简介

现在说说ORS和OFS这两个内置变量的含义。

* RS是输入记录分隔符，决定awk如何读取或分隔每行（记录）
* ORS表示输出记录分隔符，决定awk如何输出一行（记录）的，默认是回车换行（\n）
* FS是输入区域分隔符，决定awk读入一行后如何再分为多个区域。
* OFS表示输出区域分隔符，决定awk输出每个区域的时候使用什么分隔她们。
* awk无比强大，你可以通过RS，FS决定awk如何读取数据。你也可以通过修改ORS，OFS的值指定awk如何输出数据。

#### ![](/assets/21-7.png)![](/assets/21-8.png)8、字段与记录小结

现在你应该会对awk的记录字段有所了解了，下面我们总结一下，学会给阶段性知识总结是学好运维的必备技能。

![](/assets/21-5.png)

* RS记录分隔符，表示每行的结束标志
* NR行号（记录号）
* FS字段分隔符，每列的分隔标志或结束标志
* NF就是每行有多少列，每个记录中字段的数量
* $符号表示取某个列（字段）,$1$2$NF
* NF表示记录中的区域（列）数量，$NF取最后一个列（区域。）
* FS（-F）字段（列）分隔符，-F（FS）“：”&lt;==&gt;‘BEGIN{FS=':'}’
* RS 记录分隔符（行的结束标识）
* NR 行号
* 选好合适的刀FS（\*\*\*）,RS,OFS,ORS
* 分隔符==&gt;结束标识
* 记录与区域，你就对我们所谓的行与列，有了新的认识（RS，FS）

#### 9、awk基础入门总结

到了这里我们回头看看，我们之前学习的内容。

* awk的命令行结构
* awk的模式和动作
* awk的记录和字段

比较核心常用的是字段。

另外这些企业面试题可是学会awk的必备，必须自己也能写出来。

#### 练习题：

1、按单词出现频率降序排序（计算文件中每个单词的重复数量）

2、同时取出chensiqi和215379068这两个内容（指定多分隔符）

3、说说ORS和OFS这两个内置变量的含义

