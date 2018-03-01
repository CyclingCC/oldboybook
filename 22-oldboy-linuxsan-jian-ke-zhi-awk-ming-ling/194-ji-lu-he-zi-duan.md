接下来我给大家带来两个新概念记录和字段，这里为了方便大家理解可以把记录就当作行即记录==行，字段相当于列，字段==列。

![](/assets/21-12.png)

1、记录（行）

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

2、记录分隔符-RS![](/assets/21-4.png)

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

3、对$0的认识

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

