第1章 awk

1.1  awk简介

    awk不仅是linux系统中的一个命令，而且是一种编程语言，可以用来处理数据和生成报告（excel）。

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

    a、如果匹配则执行对应的动作

    b、如果不匹配条件，继续读取下一行

3、继续读取下一行

4、重复1-3，直到读取到最后一行



第2章  字段（列）和记录（行）

名称	含义

field	域，区域，字段，列

record	记录，行

2.1  域（区域，列）

	每条记录都是由多个字段组成的，默认情况下字段之间的分隔符是由空格（空格或制表符）

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

\[root@oldboy files\]\# egrep -o "\[a-zA-Z\]+" awkfile.txt \|sort \|uniq -c\|sort -nr 

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

\[root@oldboy files\]\# awk  'BEGIN{RS="\[^a-zA-Z\]+"}{print $0}' awkfile.txt \|sort \|uniq -c\|sort -nr 

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



\[root@oldboy files\]\# awk -v RS='\[:/0-9\n\]+' '{print $0}' awkfile.txt \|sort \|uniq -c\|sort -rn 

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



\[root@oldboy files\]\# awk -v RS='\[^a-Z\]+' '{print $0}' awkfile.txt \|sort \|uniq -c\|sort -rn       

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

    awk在输出整行即$0时，仅仅是原封不动的输出整行，没有任何修改，这就造成一个问题，如果我修改了OFS，那么输出整行的时候print $0  , 也不会有任何改变。

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

-----

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



