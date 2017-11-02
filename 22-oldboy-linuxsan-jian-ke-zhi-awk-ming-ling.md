第1章 awk

1.1  awk简介

```
awk不仅是linux系统中的一个命令，而且是一种编程语言，可以用来处理数据和生成报告（excel）。
```

处理的数据可以是一个或多个文件，可以是来自标准输入，也可以通过管道获取输入，awk可以在命令行上直接编辑命令进行操作，也可以编写成awk程序来进行更为复杂的运用

1.2  awk工作原理

awk  'BEGIN{ commands } pattern{ commands } END{ commands }'

第一步：执行BEGIN{ commands }语句块中的语句；

第二步：从文件或标准输入\(stdin\)读取一行，然后执行pattern{ commands }语句块，它逐行扫描文件，从第一行到最后一行重复这个过程，直到文件全部被读取完毕。

第三步：当读至输入流末尾时，执行END{ commands }语句块。

BEGIN语句块在awk开始从输入流中读取行之前被执行，这是一个可选的语句块，比如变量初始化、打印输出表格的表头等语句通常可以写在BEGIN语句块中。

END语句块在awk从输入流中读取完所有的行之后即被执行，比如打印所有行的分析结果这类信息汇总都是在END语句块中完成，它也是一个可选语句块。

pattern语句块中的通用命令是最重要的部分，它也是可选的。如果没有提供pattern语句块，则默认执行{ print }，即打印每一个读取到的行，awk读取的每一行都会执行该语句块。

示例

echo -e "A line 1nA line 2" \| awk 'BEGIN{ print "Start" } { print } END{ print "End" }'

Start

A line 1

A line 2

End

当使用不带参数的print时，它就打印当前行，当print的参数是以逗号进行分隔时，打印时则以空格作为定界符。在awk的print语句块中双引号是被当作拼接符使用，例如：

echo \| awk '{ var1="v1"; var2="v2"; var3="v3"; print var1,var2,var3; }'

v1 v2 v3

双引号拼接使用：

echo \| awk '{ var1="v1"; var2="v2"; var3="v3"; print var1"="var2"="var3; }'

v1=v2=v3

{ }类似一个循环体，会对文件中的每一行进行迭代，通常变量初始化语句（如：i=0）以及打印文件头部的语句放入BEGIN语句块中，将打印的结果等语句放在END语句块中。

1.3   awk版本

\[root@nfsserver ~\]\# cat /etc/redhat-release

CentOS release 6.7 \(Final\)

\[root@nfsserver ~\]\# uname -r

2.6.32-573.el6.x86\_64

\[root@nfsserver ~\]\# ll \`which awk\`

lrwxrwxrwx. 1 root root 4 3月   6 16:24 /bin/awk -&gt; gawk

\[root@nfsserver ~\]\# awk --version

GNU Awk 3.1.7

1.4   awk 格式

awk指令是由模式，动作，或者模式和动作的组合组成。

模式（pattern）,可以由表达式组成，也可以是两个 / 之间的正则表达式   比如 NR==1，这就是模式，可以把它理解为一个条件

动作（action）， 是由在大括号里面的一条或多条语句组成，语句之间使用  ;  隔开，格式如下

awk处理的内容可以来自标准输入 、管道、 文件

一个小例子

awk -F ":"  'NR&gt;=2 && NR&lt;=6{print NR,$1}'  /etc/passwd

2 bin

3 daemon

4 adm

5 lp

6 sync

1.5   创建环境

mkdir /server/files/ -p

head /etc/passwd &gt; /server/files/awkfile.txt

cat /server/files/awkfile.txt

\[root@nfsserver ~\]\# cat /server/files/awkfile.txt

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

1.6   awk执行过程

awk是通过一行一行的处理文件，这条命令中包含模式部分（条件）和动作部分（动作），

awk将处理模式（条件）指定的行

1、awk读入第一行内容

2、判断是否符合模式中的条件

```
a、如果匹配则执行对应的动作

b、如果不匹配条件，继续读取下一行
```

3、继续读取下一行

4、重复1-3，直到读取到最后一行

第2章  字段（列）和记录（行）

名称    含义

field    域，区域，字段，列

record    记录，行

2.1  域（区域，列）

```
每条记录都是由多个字段组成的，默认情况下字段之间的分隔符是由空格（空格或制表符）
```

来分隔，并且将分隔符记录在内置变量FS中，每行记录的字段数保存在awk的内置变量NF中

$1（第一字段）,$2（第二字段）,$3（第三字段）,$NF（最后一个字段）

$0（整行），一个记录

$ 表示取，引用某个列（区域）

FS  filed  separator  区域分隔符   awk内置变量   awk  -F  就是改变  FS 的值

NF  number  of  fileds  列的数量一行有多少列（区域）

2.2

\[root@nfsserver ~\]\# awk 'NR&gt;=2{print $0}' /server/files/awkfile.txt

bin:x:1:1:bin:/bin:/sbin/nologin

daemon:x:2:2:daemon:/sbin:/sbin/nologin

adm:x:3:4:adm:/var/adm:/sbin/nologin

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

sync:x:5:0:sync:/sbin:/bin/sync

shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown

halt:x:7:0:halt:/sbin:/sbin/halt

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin

\[root@nfsserver ~\]\# awk -F ":" 'NR&gt;=2&&NR&lt;=5{print $1,$3}' /server/files/awkfile.txt

bin 1

daemon 2

adm 3

lp 4

2.3  awk 记录（行）分隔符-RS

awk对每个要处理的输入数据认为都是具有格式和结构的，而不仅仅是一堆字符串。

默认情况下，每一行内容都成为一条记录，并以换行符结束

1、默认情况   一行 &lt;==&gt; 一个记录， 每行，都是一个记录

2、RS  ==&gt;  record  separator  输入记录（行）分隔符

3、NR  ==&gt;  number  of  record  行号，记录的数  awk当前处理着的，记录的数

4、ORS  ==&gt;  output  record  separator  输出时候的分隔符

awk使用内置变量RS来存放记录分隔符，RS表示的是输入的记录分隔符，这个值可以通过

BEGIN模块重新定义修改  在awk执行之前执行

\[root@nfsserver ~\]\# awk '{print NR,$0}' /server/files/awkfile.txt

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

\[root@nfsserver ~\]\# awk 'BEGIN{RS="/"}{print NR,$0}' /server/files/awkfile.txt

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

2.4   -v设置变量

awk -v RS="\[0-9\]+" '{print NR,$0}' awkfile.txt

1 root:x:

2 :

3 :root:/root:/bin/bash

bin:x:

4 :

5 :bin:/bin:/sbin/nologin

daemon:x:

6 :

7 :daemon:/sbin:/sbin/nologin

adm:x:

8 :

9 :adm:/var/adm:/sbin/nologin

lp:x:

10 :

11 :lp:/var/spool/lpd:/sbin/nologin

sync:x:

12 :

13 :sync:/sbin:/bin/sync

shutdown:x:

14 :

15 :shutdown:/sbin:/sbin/shutdown

halt:x:

16 :

17 :halt:/sbin:/sbin/halt

mail:x:

18 :

19 :mail:/var/spool/mail:/sbin/nologin

uucp:x:

20 :

21 :uucp:/var/spool/uucp:/sbin/nologin

说明：

在行首打印输出记录号，并打印出每一行$0的内容

awk眼中的文件是从头到尾一段连续的字符串，恰巧中间有些\n\(回车换行符\)，\n也是字符

为了方便人们的理解，awk默认就是把RS的值设置为  \n

\[root@nfsserver ~\]\# awk 'BEGIN{RS=""}{print NR,$0}' /server/files/awkfile.txt

1 root:x:0:0:root:/root:/bin/bash

bin:x:1:1:bin:/bin:/sbin/nologin

daemon:x:2:2:daemon:/sbin:/sbin/nologin

adm:x:3:4:adm:/var/adm:/sbin/nologin

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

sync:x:5:0:sync:/sbin:/bin/sync

shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown

halt:x:7:0:halt:/sbin:/sbin/halt

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin

2.5   企业案例：计算文件中每个单词的重复数量

\[root@nfsserver files\]\# sed -r 's\#\[:/0-9\]+\# \#g' awkfile.txt &gt;count.txt

\[root@nfsserver files\]\# cat count.txt

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

\[root@oldboy files\]\# cat awkfile.txt

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

\[root@oldboy files\]\# awk  'BEGIN{RS="\[:/\n0-9\]+"}{print $0}' awkfile.txt \|sort \|uniq -c\|sort -nr

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

\[root@oldboy files\]\# egrep -o "\[a-zA-Z\]+" awkfile.txt \|sort \|uniq -c\|sort -nr

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

\[root@oldboy files\]\# awk  'BEGIN{RS="\[^a-zA-Z\]+"}{print $0}' awkfile.txt \|sort \|uniq -c\|sort -nr

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

\[root@nfsserver files\]\# cat count.txt

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

\[root@nfsserver files\]\# awk 'BEGIN{RS="\( \)\|\n"}{print $0}' count.txt \|sort \|uniq -c \|sort  -rnk1

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

\[root@oldboy files\]\# awk -v RS='\[:/0-9\n\]+' '{print $0}' awkfile.txt \|sort \|uniq -c\|sort -rn

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

\[root@oldboy files\]\# awk -v RS='\[^a-Z\]+' '{print $0}' awkfile.txt \|sort \|uniq -c\|sort -rn

```
 12 sbin

 10 x

  6 nologin

  5 bin

  4 var

  3 uucp

  3 sync

  3 spool

  3 shutdown

  3 root

  3 mail

  3 halt

  3 adm

  2 lp

  2 daemon

  1 lpd

  1 bash
```

2.6   小结

1、修改了RS的值，配合NR（行）来查看变化

2、修改了FS的值，配合NF（区域，列）

3、多使用，NR, NF,  $数字，配合你调试你的awk命令

4、NR number of record 存放着每个记录的号（行号）读取新行时候会自动+1

5、RSrecoulseparator是输入数据的记录的分隔符，简单理解就是可以指定每个记录的结尾标志。

6、（用RS替换\n）

7、RS作用就是表示一个记录的结束。

8、FS标识着每个区域的结束。

2.7  awk字段（列）分隔符-FS

FS  输入字段（列）分隔符

FS   &lt;==&gt;   -F

\[root@oldboy36 files\]\# awk -F ":" '{print $1}' awkfile.txt

root

bin

daemon

adm

lp

sync

shutdown

halt

mail

uucp

\[root@oldboy36 files\]\# awk 'BEGIN{FS=":"}{print $1}' awkfile.txt

root

bin

daemon

adm

lp

sync

shutdown

halt

mail

uucp

取ip

\[root@oldboy36 files\]\# ip a s eth0\|awk -F "\[ /\]+" 'NR==3{print $3}'

10.0.0.100

\[root@oldboy36 files\]\# ip a s eth0\|awk -F "\[^0-9.\]+" 'NR==3{print $2}'

10.0.0.100

\[root@oldboy files\]\# echo "I am oldboy,my qq is 31333741"&gt;&gt;/server/files/oldboy.txt

\[root@oldboy files\]\# cat oldboy.txt

I am oldboy,my qq is 31333741

\[root@oldboy files\]\# awk -F '\[ ,\]' '{print $3,$NF}' oldboy.txt

oldboy 31333741

2.8  ORS与OFS

RS是输入记录分隔符，决定awk如何读取或分割每行（记录）

ORS表示输出记录分隔符（output record separator）,决定awk如何输出一行（记录）的，默认是回车换行  \n

FS是输入分隔符，决定awk读入一行后如何再分为多个区域

OFS表示输出分隔符，决定awk输出每个区域的时候使用什么分割

说明：

```
awk在输出整行即$0时，仅仅是原封不动的输出整行，没有任何修改，这就造成一个问题，如果我修改了OFS，那么输出整行的时候print $0  , 也不会有任何改变。
```

即：如果awk的action动作没有更改行的内容，OFS（包括ORS）都不会生效

所以我们需要让awk知道$0被修改了

$1=$1  把  $1 的值赋值给$1  这显然不会修改任何内容，但是这个动作会通知awk  我修改了$1的内容，所以再次修改print $0 时， $0的内容就变化了

\[root@oldboy32-vm1 files\]\# cat ors.txt

a

b

c

\[root@oldboy32-vm1 files\]\# awk 'BEGIN{ORS="oldboy"}{print $0}' ors.txt

aoldboyboldboyc

2.9  字段（列）和记录（行）小结

1、$ 表示取字段（列），  $1，$2    NF，$NF

2、NF  number of fileds 表示记录中的区域数量， $NF 取最后一个区域

3、FS \(-F\)  filed separator 区域分隔符，  awk -F ":" ===&gt; awk 'BEGIN{FS=":"}'

4、RS record sepatator 记录分隔符  （行的结束标识）

5、NR number of record 行号

6、选好合适的刀  FS（\*\*\*），RS， OFS,  ORS

8、$1,$3,$数字    选中你要处理的区域

9、 分隔符==&gt;结束标识

10、记录与区域，你就对我们所谓的行与列，有了新的认识（RS，FS）

11、输入支持正则，输出不支持正则

第3章 awk正则匹配

$1~/……/   $1正则匹配

$3~/……/   $3正则匹配

$4!~/....../   $4正则不匹配

\[root@nfsserver files\]\# cat count.txt

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

$3正则匹配开头为a的

\[root@nfsserver files\]\# awk '$3~/^a/{print $0}' count.txt

adm x adm var adm sbin nologin

$\(NF-1\)正则匹配以sbin结尾

\[root@nfsserver files\]\# awk '$\(NF-1\)~/sbin$/{print $0}' count.txt

bin x bin bin sbin nologin

daemon x daemon sbin sbin nologin

adm x adm var adm sbin nologin

lp x lp var spool lpd sbin nologin

shutdown x shutdown sbin sbin shutdown

halt x halt sbin sbin halt

mail x mail var spool mail sbin nologin

uucp x uucp var spool uucp sbin nologin

\[root@oldboy36 ~\]\# echo "-----1\#\#\#\#\#\#\#\#2" \|grep "\[-\#\]"

-----1\#\#\#\#\#\#\#\#2

\[root@oldboy36 ~\]\# echo "-----1\#\#\#\#\#\#\#\#2" \|grep "\[-\#\]" -o

-

-

-

-

-

\#

\#

\#

\#

\#

\#

\#

\#

\[root@oldboy36 ~\]\# echo "-----1\#\#\#\#\#\#\#\#2" \|egrep "\[-\#\]+"

-----1\#\#\#\#\#\#\#\#2

\[root@oldboy36 ~\]\# echo "-----1\#\#\#\#\#\#\#\#2" \|egrep "\[-\#\]+" -o

---

\#\#\#\#\#\#\#\#

3.1  awk正则表达式练习题

测试环境

mkdir -p /server/files/

cat &gt;&gt;/server/files/reg.txt&lt;&lt;EOF

Zhang Dandan    41117397   :250:100:175

Zhang Xiaoyu    390320151  :155:90:201

Meng  Feixue    80042789   :250:60:50

Wu    Waiwai    70271111   :250:80:75

Liu   Bingbing  41117483   :250:100:175

Wang  Xiaoai    3515064655 :50:95:135

Zi    Gege      1986787350 :250:168:200

Li    Youjiu    918391635  :175:75:300

Lao   Nanhai    918391635  :250:100:175

EOF

3.1.1 显示姓zhang的人的第二次捐款金额及他的名字

\[root@oldboy files\]\# awk -F '\[ :\]+' '$1~/Zhang/{print $2,$5}' reg.txt

Dandan 100

Xiaoyu 90

3.1.2 显示xiaoyu的姓和id号

\[root@oldboy files\]\# awk -F '\[ :\]+' '$2~/Xiaoyu/{print $1,$3}' reg.txt

Zhang 390320151

3.1.3 显示所有以41开头的id号的人的全名和id号

\[root@oldboy files\]\# awk -F '\[ :\]+' '$3~/^41.\*/{print $1,$2,$3}' reg.txt

Zhang Dandan 41117397

Liu Bingbing 41117483

3.1.4 显示所有以一个D或X开头的人名全名

\[root@oldboy files\]\# awk -F '\[ :\]+' '$2~/^\(D\|X\)/{print $1,$2}' reg.txt

Zhang Dandan

Zhang Xiaoyu

Wang Xiaoai

3.1.5 显示所有id号最后一位数字是1或5的人的全名

\[root@oldboy files\]\# awk -F '\[ :\]+' '$3~/\(1\|5\)$/{print $1,$2}' reg.txt

Zhang Xiaoyu

Wu Waiwai

Wang Xiaoai

Li Youjiu

Lao Nanhai

3.1.6 显示xiaoyu的捐款，每个值都以$开头，如$520$200$135

\[root@oldboy files\]\# awk -F '\[ :\]+' 'BEGIN{OFS="$"}$2~/Xiaoyu/{print "$"$4,$5,$6}' reg.txt

$155$90$201

3.1.7 显示所有人的全名，以姓，名的格式显示，如Meng,Feixue

\[root@oldboy files\]\# awk -F '\[ :\]+' 'BEGIN{OFS=","}{print $1,$2}' reg.txt

Zhang,Dandan

Zhang,Xiaoyu

Meng,Feixue

Wu,Waiwai

Liu,Bingbing

Wang,Xiaoai

Zi,Gege

Li,Youjiu

Lao,Nanhai

3.2  awk中替换函数

gsub\(/正则匹配/,"替换后的内容",字段\)

\[root@oldboy files\]\# awk '$2~/^Xiaoyu$/{gsub\(/:/,"$",$NF\);print $NF}' reg.txt

$155$90$201

3.3  重要思想

正则表达式如何学好  sed ， awk ， grep

通过egrep查看大致结果

通过egrep -o查看到底匹配了什么

取ip

\[root@nfsserver files\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2{print $4}'

10.0.0.31

\[root@nfsserver files\]\# ifconfig eth0\|awk -F "\(addr:\)\|\(  Bcast:\)" 'NR==2{print $2}'

10.0.0.31

取反思想

\[root@oldboy files\]\# ifconfig eth0 \|awk -F '\[^0-9.\]+' 'NR==2{print $2}'

10.0.0.10

3.4  awk支持{}的方法

--posix 或 --re-interval  使用{}时，使用

\[root@nfsserver files\]\# awk -F ":" --posix '$5~/o{1,2}/' awkfile.txt

root:x:0:0:root:/root:/bin/bash

daemon:x:2:2:daemon:/sbin:/sbin/nologin

shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown

\[root@oldgirl files\]\# awk '/o{2,3}/' passwd

\[root@oldgirl files\]\# awk --posix '/o{2,3}/' passwd

root:x:0:0:root:/root:/bin/bash

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin

operator:x:11:0:operator:/root:/sbin/nologin

postfix:x:89:89::/var/spool/postfix:/sbin/nologin

oldboooy

oldboooooooooooooooooooy

\[root@oldgirl files\]\# awk --re-interval '/o{2,3}/' passwd

root:x:0:0:root:/root:/bin/bash

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin

operator:x:11:0:operator:/root:/sbin/nologin

postfix:x:89:89::/var/spool/postfix:/sbin/nologin

oldboooy

oldboooooooooooooooooooy

正则表达式的运用，默认是在行内查找匹配的字符串，若有匹配则执行action操作，但是有时候

仅需要固定的列来匹配指定的正则表达式，比如：$ 3这一列查找匹配tom的行，这样就需要用

另外两个匹配操作符：

~ ：用于对记录或字段的表达式进行匹配

!~ : 用于表达与~相反的意思

第4章  模式匹配（条件）

4.1  awk支持的关系运算符

运算符	含义	示例

&lt;	小于	x&lt;y

&lt;=	小于或等于	x&lt;=y

==	等于	x==y

!=	不等于	x!=y

&gt;=	大于或等于	x&gt;=y

&gt;	大于	x&gt;y

以上的运算符均是针对数字，下面两个运算符针对字符串

~	与正则表达式匹配	x~/y/

!~	与正则表达式不匹配	x!~y

awk把字符串认为是变量



\[root@db02 ~\]\# awk -F : '$5=="root"' passwd 

root:x:0:0:root:/root:/bin/bash



4.2   企业案例：取出常用服务端口号

ftp，http，https，mysql， ssh端口号



\[root@nfsserver files\]\# awk -F "\[ /\]+" 'NR&gt;100&&NR&lt;120{print $2,$0}' /etc/services 

unfortunately \# unfortunately the poppassd \(Eudora\) uses a port which has already

been \# been assigned to a different service. We list the poppassd as an

alias \# alias here. This should work for programs asking for this service.

\(due \# \(due to a bug in inetd the 3com-tsmux line is disabled\)

106 \#3com-tsmux     106/tcp         poppassd

106 \#3com-tsmux     106/udp         poppassd

107 rtelnet         107/tcp                         \# Remote Telnet

107 rtelnet         107/udp

109 pop2            109/tcp         pop-2 postoffice        \# POP version 2

109 pop2            109/udp         pop-2

110 pop3            110/tcp         pop-3           \# POP version 3

110 pop3            110/udp         pop-3

111 sunrpc          111/tcp         portmapper rpcbind      \# RPC 4.0 portmapper TCP

111 sunrpc          111/udp         portmapper rpcbind      \# RPC 4.0 portmapper UDP

113 auth            113/tcp         authentication tap ident

113 auth            113/udp         authentication tap ident

115 sftp            115/tcp

115 sftp            115/udp

117 uucp-path       117/tcp

\[root@nfsserver files\]\# awk -F "\[ /\]+" '$1~/^\(ftp\|http\|https\|mysql\|ssh\)$/{print $2,$0}' /etc/services 

21 ftp             21/tcp

21 ftp             21/udp          fsp fspd

22 ssh             22/tcp                          \# The Secure Shell \(SSH\) Protocol

22 ssh             22/udp                          \# The Secure Shell \(SSH\) Protocol

80 http            80/tcp          www www-http    \# WorldWideWeb HTTP

80 http            80/udp          www www-http    \# HyperText Transfer Protocol

80 http            80/sctp                         \# HyperText Transfer Protocol

443 https           443/tcp                         \# http protocol over TLS/SSL

443 https           443/udp                         \# http protocol over TLS/SSL

443 https           443/sctp                        \# http protocol over TLS/SSL

3306 mysql           3306/tcp                        \# MySQL

3306 mysql           3306/udp                        \# MySQL

21 ftp             21/sctp                 \# FTP

22 ssh             22/sctp                 \# SSH



\[root@db02 ~\]\# awk -F "\[ /\]+" '$1~/^\(ftp\|http\|https\|mysql\|ssh\)$/{print $1,$2}' /etc/services \|uniq

ftp 21

ssh 22

http 80

https 443

mysql 3306

ftp 21

ssh 22



4.3   范围模式

awk '/start pos/,/end pos/{pint $0}' passwd

awk '/start pos/,NR==xxx{print $0}' passwd

范围模式的时候，范围条件的时候，表达式必须能匹配一行





\[root@nfsserver files\]\# sed -n '2,5p' count.txt

bin x bin bin sbin nologin

daemon x daemon sbin sbin nologin

adm x adm var adm sbin nologin

lp x lp var spool lpd sbin nologin

\[root@nfsserver files\]\# awk 'NR==2,NR==5{print NR,$0}' count.txt

2 bin x bin bin sbin nologin

3 daemon x daemon sbin sbin nologin

4 adm x adm var adm sbin nologin

5 lp x lp var spool lpd sbin nologin



\[root@nfsserver files\]\# sed -n '/^bin/,/^lp/p' count.txt 

bin x bin bin sbin nologin

daemon x daemon sbin sbin nologin

adm x adm var adm sbin nologin

lp x lp var spool lpd sbin nologin

\[root@nfsserver files\]\# awk '/^bin/,/^lp/{print NR,$0}' count.txt 

2 bin x bin bin sbin nologin

3 daemon x daemon sbin sbin nologin

4 adm x adm var adm sbin nologin

5 lp x lp var spool lpd sbin nologin

4.4  小结

1、模式===&gt;条件

2、正则表达式

3、条件表达式（NR&gt;=2   NR==2）

4、范围表达式 \( NR==2，NR==5    /正则表达式-开始/，/正则结束/  \)

7、$1~/正则表达式-开始/,$3~/正则结束/ 

8、列，区域：FS 刀分隔符，FS区域分隔符

9、行，记录: RS 刀分隔符，RS记录分隔符

10、 FS====&gt;  NF 区域，列的数量

11、 RS====&gt;  NR  记录号，随着记录的增加 NR 自动+1



第5章  awk  BEGIN模块

BEGIN模块在awk读取文件之前就执行，一般用来定义我们的内置变量（FS,RS等）

可以输出表头（excel表格名称）

BEGIN模块可以做一些测试，如算术运算



\[root@oldboy files\]\# awk 'BEGIN{print 10/3}'

3.33333



第6章  awk  END模块

END在awk读取完所有文件的时候，再执行END模块，一般用来输出一个结果（累加，数组结果），

也可以是和BEGIN模块类似的结尾标识信息



注意 BEGIN或END模块只能有一个

模式{动作}  可以是多个

'NR==2{print $1}NR==5{print $0}'

awk  -F  ":"  'NR==1{print NR,$0}NR==2{print NR,$NF}'  awkfile.txt



第7章  awk编程思想

1、awk核心思想就是先处理，然后END模块输出   （ 累加（a++;a+=$0）,awk数组 ）

2、BEGIN模块用于awk内置变量 FS, RS的赋值，打印标题头信息 （excel表格里面标题行）

要在awk执行前，定义好

3、END模块用来最后输出，统计信息，awk数组信息  （累加（a++;a+=$0） awk数组）

\[root@oldboy files\]\# cat awkfile.txt 

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

\[root@oldboy files\]\# awk -F : 'BEGIN{print "user","UID"}{print $1,$3}' awkfile.txt \|column -t

user      UID

root      0

bin       1

daemon    2

adm       3

lp        4

sync      5

shutdown  6

halt      7

mail      8

uucp      10



awk 'BEGIN{print "hello world!"}{print NR,$0}END{print "end of file"}' count.txt 

hello world!

1 root x root root bin bash

2 bin x bin bin sbin nologin

3 daemon x daemon sbin sbin nologin

4 adm x adm var adm sbin nologin

5 lp x lp var spool lpd sbin nologin

6 sync x sync sbin bin sync

7 shutdown x shutdown sbin sbin shutdown

8 halt x halt sbin sbin halt

9 mail x mail var spool mail sbin nologin

10 uucp x uucp var spool uucp sbin nologin

end of file

统计/etc/services文件里面的空行数量

\[root@nfsserver files\]\# awk '$0~/^$/{a++}END{print a}' /etc/services 

16

\[root@oldboy files\]\# grep -c "^$" /etc/services 

16

企业面试题： awkfile2.txt里面以:为分隔符，区域3大于15，一共有多少行？

\[root@nfsserver files\]\# head -20 /etc/passwd &gt; awkfile2.txt 

\[root@nfsserver files\]\# awk -F ":" '$3&gt;15{a+=1;print a}' awkfile2.txt 

1

2

3

4

5

6

\[root@nfsserver files\]\# awk -F ":" '$3&gt;15{a+=1}END{print a}' awkfile2.txt  

6

7.1   a++

a=a+1    ==&gt;  a++

a=a+2    ==&gt;  a+=2

a=a+$0   ==&gt;  a+=$0

\[root@nfsserver files\]\# seq 100 \| awk '{a=a+$0}END{print "the result is:"a }'

the result is:5050

\[root@oldboy files\]\# seq 5

1

2

3

4

5

\[root@oldboy files\]\# seq 5 \|awk  '{sum=sum+$0}END{print sum}'

15

7.2   企业案例

找出环境变量$PATH中，所有只有三个任意字符的命令，例如tee，并将他们重定向到

command.txt中，要求一行显示1个，并在文件尾部统计他们的个数



通配符：用来匹配文件名的  {}字符序列

正则表达：字符串



\[root@nfsserver ~\]\# find $\(echo $PATH \|tr ":" " "\) -type f -name "???" 2&gt;/dev/null \|awk '{a++}END{print a}' 

69

第8章 awk基本结构



awk  'BEGIN{}/pattern/{coms}END{coms}'



awk执行过程



1、命令行的赋值（-F 或 -v）

2、执行BEGIN模式里面的内容

3、开始读取文件

4、判断条件（模式）是否成立

   成立则执行对应动作里面的内容

   读取下一行，循环判断

   直到读取到最后一个文件的结尾

5、最后执行END模式里面的内容

6、结束





\[root@nfsserver files\]\# awk -F ":" 'NR==1{print NR,$0}NR==2{print NR,$NF"second line"}' awkfile.txt 

1 root:x:0:0:root:/root:/bin/bash

2 /sbin/nologinsecond line



第9章  awk内置变量（预定义变量）

变量名	属性

$0	当前记录，一整行

$1，$2，$3，...$n	当前记录的第n个字段，字段间由FS分隔

FS	输入字段分隔符  默认是空格

NF	当前记录中的字段个数，就是有多少列

NR	已经读出的记录数，就是行号，从1开始

RS	输入的记录分隔符默认为换行符

OFS	输出字段分隔符  默认是空格

ORS	输出的记录分隔符  默认是换行符

FNR	当前文件的读入记录号

FILENAME	当前正在处理的文件的文件名

\[root@nfsserver files\]\# awk '{print FILENAME,NR,FNR}' awkfile.txt  count.txt 

awkfile.txt 1 1

awkfile.txt 2 2

awkfile.txt 3 3

awkfile.txt 4 4

awkfile.txt 5 5

awkfile.txt 6 6

awkfile.txt 7 7

awkfile.txt 8 8

awkfile.txt 9 9

awkfile.txt 10 10

count.txt 11 1

count.txt 12 2

count.txt 13 3

count.txt 14 4

count.txt 15 5

count.txt 16 6

count.txt 17 7

count.txt 18 8

count.txt 19 9

count.txt 20 10

第10章 awk数组

10.1 数组结构

      数组名\[下标\] =值

arrayname\[string\]=value

10.2  awk一些实例

\[root@nfsserver files\]\# awk 'BEGIN{man="woman";print man}'   

woman

\[root@nfsserver files\]\# awk 'BEGIN{man="woman woman2 woman3";print man}' 

woman woman2 woman3

\[root@nfsserver files\]\# awk 'BEGIN{kuang\[1\]="woman";kuang\[2\]="woman2";kuang\[3\]="woman3";print kuang\[1\],kuang\[2\],kuang\[3\]}'

woman woman2 woman3



\[root@oldboy36 ~\]\# awk 'BEGIN{kuang\[a\]="woman";kuang\[b\]="woman2";kuang\[c\]="woman3";print a,kuang\[a\],b,kuang\[b\],c,kuang\[c\]}'

 woman3  woman3  woman3

\[root@oldboy36 ~\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3";print a,kuang\["a"\],b,kuang\["b"\],c,kuang\["c"\]}'

 woman  woman2  woman3

10.3  awk数组说明

1、shell与awk中变量默认值为空

2、kuang\[a\]  kuang\[b\]  kuang\[c\] 中的a、 b、c 被认为是变量，都没有赋值，默认为空

   所以 kuang\[a\]  kuang\[b\]  kuang\[c\]  是同一个元素，最终结果相同

3、数组元素名为字符串时必须用""  kuang\["a"\]  kuang\["b"\]  kuang\["c"\]

4、awk数组中的元素不一定是连续的，这点不同于其他语言的数组 

第11章  awk中的for

循环   变量           数组名

for\(key  in  array\)

             关键字

key遍历array数组的下标

11.1  一些实例

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print shou}' awkfile.txt       

a

b

c

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print kuang\[shou\]}' awkfile.txt 

woman

woman2

woman3

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print shou,kuang\[shou\]}' awkfile.txt 

a woman

b woman2

c woman3

11.2  企业面试题

处理以下文件内容，将域名取出并根据域名进行计数排序处理（去重）：（百度和sohu面试题）



\[root@nfsserver files\]\# cat mianshi.txt 

http://www.etiantian.org/index.html

http://www.etiantian.org/1.html

http://post.etiantian.org/index.html

http://mp3.etiantian.org/index.html

http://www.etiantian.org/3.html

http://post.etiantian.org/2.html

\[root@nfsserver files\]\# awk -F "/+" '{kuang\[$2\]++;print NR,$2,kuang\["www.etiantian.org"\]}' mianshi.txt 

1 www.etiantian.org 1

2 www.etiantian.org 2

3 post.etiantian.org 2

4 mp3.etiantian.org 2

5 www.etiantian.org 3

6 post.etiantian.org 3



\[root@nfsserver files\]\# awk -F "/+" '{kuang\[$2\]++}END{for\(shou in kuang\) print shou,kuang\[shou\]}' mianshi.txt 

mp3.etiantian.org 1

post.etiantian.org 2

www.etiantian.org 3



\[root@db02 ~\]\# cat sort.txt 

http://www.etiantian.org/index.html

http://www.etiantian.org/1.html

http://post.etiantian.org/index.html

http://mp3.etiantian.org/index.html

http://www.etiantian.org/3.html

http://post.etiantian.org/2.html

\[root@db02 ~\]\# awk -F "\[/.\]+" '{hotel\[$2\]++}END{for\(police in hotel\)print police,hotel\[police\]}' sort.txt 

www 3

mp3 1

post 2



\[root@oldboy files\]\# cat mianshi.txt 

http://www.etiantian.org/index.html

http://www.etiantian.org/1.html

http://post.etiantian.org/index.html

http://mp3.etiantian.org/index.html

http://www.etiantian.org/3.html

http://post.etiantian.org/2.html



先处理，再输出

\[root@oldboy files\]\# awk -F '\[:/\]+' '{a\[$2\]++}END{for\(i in a\) print a\[i\],i }' mianshi.txt\|sort -r 

3 www.etiantian.org

2 post.etiantian.org

1 mp3.etiantian.org



\[root@oldboy36 files\]\# cat url.txt 

http://www.etiantian.org/index.html

http://www.etiantian.org/1.html

http://post.etiantian.org/index.html

http://mp3.etiantian.org/index.html

http://www.etiantian.org/3.html

http://post.etiantian.org/2.html

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{print $2}' url.txt 

www

www

post

mp3

www

post

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["www"\],"www"}' url.txt 

3 www

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["post"\],"post"}' url.txt 

2 post

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["mp3"\],"mp3"}' url.txt 

1 mp3

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{for\(i in h\)print h\[i\],i}' url.txt 

3 www

1 mp3

2 post



\[root@db02 files\]\# awk -F "\[\(\)&lt;&gt;\]" '/^2016/{qi\[$\(NF-1\)\]++}END{for\(key in qi\) print key,qi\[key\]}' 31\_group.txt \|sort -rn -k2

aini8867758258@yahoo.cn 252

2934145242 154

764539136 147

5257409 137

a1046186419@qq.com 121

390320151 99

273558676 96

805022948 85

41117483 82

86988614 79

1226032602 60

10000 57

987766870 56

610010167 54

619876714 41

13216056 40

156322285 37

714900946 36

351319663 36

27061859 36

2051510479 35

1354372178 33

380926619 32

215956299 31

632528468 30



\[root@db02 files\]\# seq 100 \|awk '{sum+=$1}END{print sum}'

5050

11.3  【统计文件中单词个数】\*\*\*\*\*\*\*\*\*

\[root@oldboy files\]\# cat awkfile.txt 

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

\[root@oldboy files\]\# awk -v RS="\[^a-Z\]+" '{a\[$1\]++}END{for\(i in a\) print a\[i\],i}' awkfile.txt \|sort -nr\|column -t

12  sbin

10  x

6   nologin

5   bin

4   var

3   uucp

3   sync

3   spool

3   shutdown

3   root

3   mail

3   halt

3   adm

2   lp

2   daemon

1   lpd

1   bash

11.4  小结

1、awk数组，去重

2、选好分隔符 -F "/+"

3、选好处理的区域，print $1,$3,$2

4、kuang\[$2\]++  =====&gt; a++ 

5、awk数组的一个处理思想，先处理，最后END模块输出

6、输出awk数组使用for\(shou in kuang\)  \#自动摸索



11.5   awk相关英语总结

field	域，区域，字段

record	记录，默认一整行

field separator	FS：区域分隔符，表示一个区域的结束，字段，域

number of record	NR: 记录号

number of field	NF：每一个记录中区域的数量

record separator	RS：记录分隔符，标识每个记录的结束

output field separator	OFS

output record separator	ORS

file number of record	FNR  awk当前处理的文件的记录号



awk '{h\[$1,$7\]++}END{for\(key in h\) print key,h\[key\]}' filename 

深入浅出linux三剑客之awk必杀技一例

http://oldboy.blog.51cto.com/2561410/950730



第12章 awk内置函数

12.1  gsub

gsub\(/正则匹配/,"替换后的内容",字段\)

\[root@oldboy files\]\# awk '$2~/^Xiaoyu$/{gsub\(/:/,"$",$NF\);print $NF}' reg.txt 

$155$90$201



12.2  substr

substr\(某一列,从第几个符号,几个字母\)

echo abcdefghi \|awk '{print substr\($1,6,2\)}'

fg



12.3  split

精确切割

split\(s, a \[, r\]\)

split\(某一列,数组名字,/正则表达式/\)

\#把某一列通过正则表达式切割，切完后放到数组中

\#注意:数组元素是从1开始



echo GET /mobile/theme/oldboy/common/images/arrow-down2.png

GET /mobile/theme/oldboy/common/images/arrow-down2.png



echo GET /mobile/theme/oldboy/common/images/arrow-down2.png \|awk '{split\($2,arr,/\./\);print arr\[1\]}'

/mobile/theme/oldboy/common/images/arrow-down2



echo GET /mobile/theme/oldboy/common/images/arrow-down2.png \|awk '{split\($2,arr,/\./\);print arr\[2\]}'

png



echo GET /mobile/theme/oldboy/common/images/arrow-down2.png \|awk '{split\($2,arr,/\./\);print arr\[1\],arr\[2\]}'

/mobile/theme/oldboy/common/images/arrow-down2 png



echo GET /mobile/theme/oldboy/common/images/arrow-down2.png \|awk '{split\($2,arr,/\./\);for\(i in arr\) print i}'

1

2

echo GET /mobile/theme/oldboy/common/images/arrow-down2.png \|awk '{split\($2,arr,/\./\);for\(i in arr\) print i,arr\[i\]}'

1 /mobile/theme/oldboy/common/images/arrow-down2

2 png

第13章  awk总结

13.1  awk工作原理

13.2  BEGIN 与  END

BEGIN模块输出一些提示性文字  awk内置变量FS,RS,ORS,OFS

END模块输出一些提示性文字，显示最后的结果，计算空行，awk数组，取苹果的过程把苹果

展示处理

awk里面的普通变量不用初始化

awk先处理，一行一行处理，然后END模块输出

13.3  域、记录

FS 指定各种各样的刀（正则表示），RS 正则表示

13.4  模式匹配 ===&gt; 条件

正则表达式

^ 字符串开头

$ 字符串结尾

$3~/^https/

--posix 或 --re-interval

NR==1

NR&gt;=2

模式默认匹配  一行  $0

$3~/^r/

/reg/ 默认匹配整行  $0

awk '$3~/\[4-6\]/{print $0}'

范围匹配

NR==2，NR==5   ====&gt;   2,5p

/start位置/,/结束位置/

显示Dan第二次捐款金额

显示TOM的名字和电话号码

显示所有以138开头的号码的人的全名和手机号码

显示所有以一个C或E开头的人名

显示所有手机号码最后数字是1或5的人名

显示Chet的捐款.每个值时都有以$开头.如$520$200$135 

显示姓,其后跟一个逗号和名,如Jody,Savage

\[root@db02 files\]\# cat reg.txt 

Mike Harrington:     13716352255 :250:100:175

Christian Dobbins:   13901284715 :155:90:201

Susan Dalsass:       13810756741 :250:60:50

Nancy McNeil:        13810862484 :250:80:75

John Goldenrod:      13521156269 :250:100:175

Chet Main:           13810733714 :50:95:135

Tom Savage:          13716052112 :250:168:200

Elizabeth Stachelin: 18811233838 :175:75:300

Archie McNichol:     13520593076 :250:100:175

Jody Savage:         13716802727 :15:188:150

Guy Quigley:         13520321021 :250:100:175

Dan Savage:          13716375331 :450:300:275

\[root@db02 files\]\# awk -F "\[ :\]+" '$1~/Dan/{print $\(NF-1\)}' reg.txt  

300

\[root@db02 files\]\# awk -F "\[ :\]+" '$1~/Tom/{print $1,$3}' reg.txt 

Tom 13716052112

\[root@db02 files\]\# awk -F "\[ :\]+" '$3~/^138/{print $1,$2,$3}' reg.txt     

Susan Dalsass 13810756741

Nancy McNeil 13810862484

Chet Main 13810733714

\[root@db02 files\]\# awk  '$1~/^\(C\|E\)/{print $1}' reg.txt 

Christian

Chet

Elizabeth

\[root@db02 files\]\# awk -F "\[ :\]+" '$1~/Chet/{print $1,"$"$4,"$"$5,"$"$6}' reg.txt 

Chet $50 $95 $135

\[root@db02 files\]\# awk -F "\[ :\]+" '{print $2","$1}' reg.txt  

Harrington,Mike

Dobbins,Christian

Dalsass,Susan

McNeil,Nancy

Goldenrod,John

Main,Chet

Savage,Tom

Stachelin,Elizabeth

McNichol,Archie

Savage,Jody

Quigley,Guy

Savage,Dan



13.5  轻松精通awk数组企业问题案例

http://oldboy.blog.51cto.com/2561410/1687026

\[root@show test\_2016-05-11\]\# cat pro1.txt 

a 1

b 2

c 3

d 5

a 3

c 4

c 9

d 1

awk '{kuang\[$1\]+=$2}END{for\(shou in kuang\)print shou,kuang\[shou\]}'  pro1.txt 

a 4

b 2

c 16

d 6

\[root@db02 files\]\# cat add.txt 

a  1

b  3

c  2

d  7

b  5

a  3 

g  2

f  6

d  9

\[root@db02 files\]\# awk '{a\[$1\]+=$2}END{for\(i in a\)print i,a\[i\]}' add.txt 

a 4

b 8

c 2

d 16

f 6

g 2

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{print $0}'  pro3.txt 

root

x

root

root

bin

bash

bin

x

bin

bin

sbin

nologin

daemon

x

daemon

sbin

sbin

nologin

adm

x

adm

var

adm

sbin

nologin

lp

x

lp

var

spool

lpd

sbin

nologin

sync

x

sync

sbin

bin

sync

shutdown

x

shutdown

sbin

sbin

shutdown

halt

x

halt

sbin

sbin

halt

mail

x

mail

var

spool

mail

sbin

nologin

uucp

x

uucp

var

spool

uucp

sbin

nologin

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++;print $1,kuang\[$1\]}'  pro3.txt 

root 1

x 1

root 2

root 3

bin 1

bash 1

bin 2

x 2

bin 3

bin 4

sbin 1

nologin 1

daemon 1

x 3

daemon 2

sbin 2

sbin 3

nologin 2

adm 1

x 4

adm 2

var 1

adm 3

sbin 4

nologin 3

lp 1

x 5

lp 2

var 2

spool 1

lpd 1

sbin 5

nologin 4

sync 1

x 6

sync 2

sbin 6

bin 5

sync 3

shutdown 1

x 7

shutdown 2

sbin 7

sbin 8

shutdown 3

halt 1

x 8

halt 2

sbin 9

sbin 10

halt 3

mail 1

x 9

mail 2

var 3

spool 2

mail 3

sbin 11

nologin 5

uucp 1

x 10

uucp 2

var 4

spool 3

uucp 3

sbin 12

nologin 6

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++;print $1"\t"kuang\[$1\]}'  pro3.txt 

root	1

x	1

root	2

root	3

bin	1

bash	1

bin	2

x	2

bin	3

bin	4

sbin	1

nologin	1

daemon	1

x	3

daemon	2

sbin	2

sbin	3

nologin	2

adm	1

x	4

adm	2

var	1

adm	3

sbin	4

nologin	3

lp	1

x	5

lp	2

var	2

spool	1

lpd	1

sbin	5

nologin	4

sync	1

x	6

sync	2

sbin	6

bin	5

sync	3

shutdown	1

x	7

shutdown	2

sbin	7

sbin	8

shutdown	3

halt	1

x	8

halt	2

sbin	9

sbin	10

halt	3

mail	1

x	9

mail	2

var	3

spool	2

mail	3

sbin	11

nologin	5

uucp	1

x	10

uucp	2

var	4

spool	3

uucp	3

sbin	12

nologin	6

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++}END{for\(shou in kuang\)print shou,kuang\[shou\]}'  pro3.txt 

nologin 6

bin 5

uucp 3

mail 3

sync 3

x 10

spool 3

var 4

shutdown 3

adm 3

lpd 1

daemon 2

halt 3

root 3

bash 1

lp 2

sbin 12

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++}END{for\(shou in kuang\)print shou,kuang\[shou\]}'  pro3.txt  \| sort -rnk2 

sbin 12

x 10

nologin 6

bin 5

var 4

uucp 3

sync 3

spool 3

shutdown 3

root 3

mail 3

halt 3

adm 3

lp 2

daemon 2

lpd 1

bash 1





13.6  awk 二维数组

awk '{s\_num\[$1,$7\]++;s\_size\[$1,$7\]+=$10}{for\( i in s\_num\)split\(i,idx,SUBSEP\);{print s\_num\[idx\[1\],idx\[2\]\],idx\[1\],idx\[2\],s\_size\[idx\[1\],idx\[2\]\]}}' access1.log













第14章  附

原数据文件：

id=aa&bb&type&name=cc

bb&id=aa&name=cc&type

id=aa&type&bb&name=dd

type&id=aa&cc&name=bb

id=bb&cc&type&name=bb

aa&id=bb&name=bb&type





整理并去重,得到效果：

id=aa&bb&name=cc&type

id=aa&bb&name=dd&type

id=aa&cc&name=bb&type

id=bb&cc&name=bb&type

id=bb&aa&name=bb&type





awk --posix 'BEGIN{OFS=FS="&"}

{

  for\(i=1;i&lt;=NF;i++\)

    {if\($i~/^id=.\*$/\){a=$i};

     if\($i~/^\[a-z\]{2}$/\){b=$i};

    if\($i~/^\[a-z\]{4}$/\){c=$i};

    if\($i~/^name=.\*$/\){d=$i}};

    print a,b,d,c}'

 file.txt \|sort\|uniq



















awk打印99乘法表

\[root@oldboy36 ~\]\# awk 'BEGIN{for\(x=1;x&lt;=9;x++\){for\(i=1;i&lt;=x;i++\){printf i"x"x"="i\*x" "}print}}' \|column -t

1x1=1

1x2=2  2x2=4

1x3=3  2x3=6   3x3=9

1x4=4  2x4=8   3x4=12  4x4=16

1x5=5  2x5=10  3x5=15  4x5=20  5x5=25

1x6=6  2x6=12  3x6=18  4x6=24  5x6=30  6x6=36

1x7=7  2x7=14  3x7=21  4x7=28  5x7=35  6x7=42  7x7=49

1x8=8  2x8=16  3x8=24  4x8=32  5x8=40  6x8=48  7x8=56  8x8=64

1x9=9  2x9=18  3x9=27  4x9=36  5x9=45  6x9=54  7x9=63  8x9=72  9x9=81





学习正则表达式，一定要通过

grep或egrep学习  配合 egrep -o  

alias grep='grep --color=auto'

alias egrep='egrep --color=auto'





awk调试工具  pgawk

