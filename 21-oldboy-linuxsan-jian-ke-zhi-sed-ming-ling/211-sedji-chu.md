### 一、sed基础

#### 1、sed简介

sed是stream editor（字符流编辑器）的缩写，简称流编辑器。什么是流呢？大家可以想象一下流水线，sed就像一个车间一样，文件中的每行字符都是原料，运到sed车间，然后经过一系列的加工处理，最后从流水线下来就变成货物了

![](/assets/20-1.png)

#### 2、sed功能

sed命令是操作、过滤和转换文本内容的强大工具。常用功能有增删改查（增加、删除、修改、查询），其中查询的功能中最常用的两大功能是过滤（过滤指定字符串），取行（取出指定行）

我们现在准备学习的sed版本是GNU开源版本的，我的实验环境是Centos6.7系统，内核版本是  2.6.32-573.el6.x86\_64

\[root@oldboy ~\]\# cat /etc/redhat-release

CentOS release 6.7 \(Final\)

\[root@oldboy ~\]\# uname -r

2.6.32-573.el6.x86\_64

\[root@oldboy ~\]\# sed --version

GNU sed version 4.2.1

#### 3、语法格式

sed  \[option\]  '\[sed-commands\]'  \[input-file\]

sed  \[选项\]   '\[sed命令\]'       \[输入文件\]

![](/assets/tab20-4.png)说明：

1）注意sed软件以及后面选项、sed命令和输入文件，每个元素之间都至少有一个空格

2）为了避免混淆，sed 称为 sed软件 ，sed-commands（sed命令）是sed软件内置的一些命令选项，为了和前面的options（选项）区分，故称为sed命令

3）sed-commands既可以是单个sed命令，也可以是多个sed命令组合

4）input-file（输入文件）是可选的，sed还能够从标准输入如管道获取输入

#### 4、命令执行流程

sed软件从文件或管道中读取一行，处理一行，输出一行；再读取一行，再处理一行，再输出一行 ......

小知识：一次一行的设计使得sed软件性能很高，sed在读取非常庞大的文件时不会出现卡顿的现象。大家都用过vi命令，用vi命令打开几十M或更大的文件，会发现卡顿现象，这是因为vi命令打开文件是一次性将文件加载到内存，然后在打开，因此卡顿的时间长短就取决于从磁盘到内存的读取速度。而且如果文件过大的话还会造成内存溢出现象。sed软件就很好的避免了这种情况，打开速度非常快，执行速度也很快

![](/assets/20-2.png)

#### 5、sed命令

![](/assets/tab20-5.png)

#### 6、sed特殊符号

![](/assets/tab20-6.png)

### 二、sed增删改查

#### 1、创建环境

cat &gt;person.txt&lt;&lt;EOF

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

EOF

#### 2、增

##### a 追加文本到指定行后； apend 追加 {#a--追加文本到指定行后；--apend--追加}

##### i 插入文本到指定行前； insert 插入 {#i--插入文本到指定行前；---insert--插入}

\[root@oldboy ~\]\# cat person.txt

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### \[root@oldboy ~\]\# sed '2a 106,dandan,CSO' person.txt {#rootoldboy--sed-2a-106dandancso-persontxt}

101,oldboy,CEO

102,zhangyao,CTO

106,dandan,CSO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### \[root@oldboy ~\]\# sed '2i 106,dandan,CSO' person.txt {#rootoldboy--sed-2i-106dandancso-persontxt}

101,oldboy,CEO

106,dandan,CSO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### \[root@oldboy ~\]\# sed '2a 106,dandan,CSO\n107,bingbing,CCO' person.txt {#rootoldboy--sed-2a-106dandancson107bingbingcco-persontxt}

101,oldboy,CEO

102,zhangyao,CTO

106,dandan,CSO

107,bingbing,CCO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

sed '2a 106,dandan,CSO \

107,bingbing,CCO' person.txt

101,oldboy,CEO

102,zhangyao,CTO

106,dandan,CSO

107,bingbing,CCO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### 多行增

\[root@oldboy ~\]\# echo -e "oldboy\noldboy"

oldboy

oldboy

##### 企业案例1：优化SSH配置（一键完成增加若干参数）

在我们学习CentOS6系统优化时，有一个优化点：更改ssh服务远程登录的配置。主要的操作是在ssh的配置文件/etc/ssh/sshd\_config加入下面5行文本。\(下面参数的具体含义见其他课程。\)

Port 52113

PermitRootLogin no

PermitEmptyPasswords no

UseDNS no

GSSAPIAuthentication no

当然我们可以使用vi/vim命令编辑这个文本，但这样就比较麻烦，现在想一条命令增加5行文本到第13行前？

解答：

sed -i '13i Port 52113\nPermitRootLogin no\nPermitEmptyPasswords no\nUseDNS no\nGSSAPIAuthentication no' sshd\_config

\[root@oldboy ~\]\# echo A{,.ori}

A A.ori

##### { } 作用

![](https://www.luffycity.com/linux-book/assets/20-3.png)

##### 调试工具sedsed命令

安装sedsed命令

wget[http://sedsed.sourceforge.net/sedsed-1.0](http://sedsed.sourceforge.net/sedsed-1.0)-O /bin/sedsed

PATT是pattern模式的缩写，即模式空间

HOLD是保持空间

COMM是command的缩写，即sed命令

sedsed -d --hide=hold "2i 106,dandan,CSO" person.txt

#### 3、删

d 删除行 delete

\[root@oldboy ~\]\# sed '3d' person.txt

101,oldboy,CEO

102,zhangyao,CTO

104,yy,CFO

105,feixue,CIO

\[root@oldboy ~\]\# sed '1,3d' person.txt

104,yy,CFO

105,feixue,CIO

\[root@oldboy ~\]\# sed '1,+3d' person.txt

105,feixue,CIO

\[root@oldboy ~\]\# sed '1~3d' person.txt

102,zhangyao,CTO

103,Alex,COO

105,feixue,CIO

\[root@oldboy ~\]\# sed '3,$d' person.txt

101,oldboy,CEO

102,zhangyao,CTO

\[root@oldboy ~\]\# sed '/oldboy/d' person.txt

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### 地址范围

sed软件可以对单行或多行文本进行处理。如果在sed命令前面不指定地址范围，那么默认会匹配所有行

用法： n1\[,n2\]{sed-commands}

地址用逗号分隔，n1,n2 可以用数字、正则表达式、或者二者的组合表示

![](https://www.luffycity.com/linux-book/assets/tab20-7.png)

#### 4、改

##### 1）按行替换

c 用新行取代旧行 c change

\[root@oldboy ~\]\# sed '2c 106,dandan,CSO' person.txt

101,oldboy,CEO

106,dandan,CSO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

##### 2）字符串替换

s：单独使用→将每一行中第一处匹配的字符串进行替换 ==&gt;sed命令

g：每一行进行全部替换 ==&gt;sed命令s的替换标志之一，非sed命令

-i：修改文件内容 ==&gt;sed软件的选项

sed软件替换模型\(方框▇被替换成三角▲\)

sed 's/▇/▲/g' oldboy.log

sed 's\#▇\#▲\#g' oldboy.log

观察特点

1两边是引号，引号里面的两边分别为s和g，中间是三个一样的字符/或\#作为定界符。\#能在替换内容包含/有助于区别。定界符可以是任意符号如:或\|等，但当替换内容包含定界符时，需转义即: \|。经过长期实践，建议大家使用\#作为定界符。

2、定界符/或\#，第一个和第二个之间的就是被替换的内容，第二个和第三个之间的就是替换后的内容。

3、 s\#▇\#▲\#g，▇能用正则表达式，但▲不能用，必须是具体的。

4、默认sed软件是对模式空间\(内存中的数据\)操作，而-i选项会更改磁盘上的文件内容。

##### \[root@oldboy ~\]\# sed '2s@^\#@@' /var/spool/cron/root 开头的\#去掉 {#rootoldboy--sed-2s-varspoolcronroot-------开头的去掉}

\#print my name

\* \* \* \* \* /bin/echo dongzhi &gt;&gt;/server/log/dongzhi

\[root@oldboy ~\]\# sed -i '2s@^\#@@' /var/spool/cron/root

\[root@oldboy ~\]\# cat /var/spool/cron/root

\#print my name

\* \* \* \* \* /bin/echo dongzhi &gt;&gt;/server/log/dongzhi

##### \[root@oldboy ~\]\# sed 's@^@\#@' /var/spool/cron/root 开头添加\ {#rootoldboy--sed-s-varspoolcronroot--------开头添加}

\#\#print my name

\#\* \* \* \* \* /bin/echo dongzhi &gt;&gt;/server/log/dongzhi

\[root@oldboy ~\]\# sed -i 's@^@\#@' /var/spool/cron/root

\[root@oldboy ~\]\# cat /var/spool/cron/root

\#\#print my name

\#\* \* \* \* \* /bin/echo dongzhi &gt;&gt;/server/log/dongzhi

##### \[root@oldboy ~\]\# sed '3s\#0\#9\#' person.txt {#rootoldboy--sed-3s09-persontxt}

101,oldboy,CEO

102,zhangyao,CTO

193,Alex,COO

104,yy,CFO

105,feixue,CIO

##### 3）使用s命令替换为空

\[root@iZ25hfz3698Z ~\]\# stat /etc/hosts

File: \`/etc/hosts'

Size: 125 Blocks: 8 IO Block: 4096 regular file

Device: ca01h/51713d Inode: 918496 Links: 1

Access: \(0644/-rw-r--r--\) Uid: \( 0/ root\) Gid: \( 0/ root\)

Access: 2016-11-22 17:54:13.536012781 +0800

Modify: 2015-03-30 09:10:50.982117786 +0800

Change: 2015-03-30 09:10:50.982117786 +0800

\[root@iZ25hfz3698Z ~\]\# stat /etc/hosts\|sed -nr '$s\#^.\*ge: \| \[0-9\]{2}.\*$\#\#gp'

2015-03-30

##### 4）变量替换

\[root@oldboy ~\]\# cat test.txt

a

b

a

\[root@oldboy ~\]\# x=a;y=b

\[root@oldboy ~\]\# sed "s\#$y\#$x\#" test.txt

a

a

a

##### 5）特殊命令 eval

\[root@oldboy ~\]\# eval sed 's\#$y\#$x\#' test.txt

a

a

a

##### 6）分组替换

sed软件的\\(\\)的功能可以记住正则表达式的一部分，其中， \1为第一个记住的模式

即第一个小括号中匹配的内容， \2为第二个记住的模式，即第二个小括号中匹配的内容，

sed最多可以记住9个

关闭开机自启动的服务

chkconfig --list \|grep "3:on"\|egrep -v "sshd\|crond\|network\|rsyslog\|sysstat"\|awk '{print $1}'\|sed -r 's\#\(^.\*\)\#chkconfig \1 off\#g'\|bash

##### 7）sed软件s命令中的特殊符号&

&代表s\#\#\#g 中前两个\# 之间的全部内容

##### 8）批量修改文件名

touch stu\_102999\_{1..5}\_finished.jpg

\[root@oldboy test\]\# ls\|xargs -n1 \|sed -r 's\#\(^.\*\)\_finished\(.\*\)\#mv & \1\2\#g'

mv stu\_102999\_1\_finished.jpg stu\_102999\_1.jpg

mv stu\_102999\_2\_finished.jpg stu\_102999\_2.jpg

mv stu\_102999\_3\_finished.jpg stu\_102999\_3.jpg

mv stu\_102999\_4\_finished.jpg stu\_102999\_4.jpg

mv stu\_102999\_5\_finished.jpg stu\_102999\_5.jpg

\[root@oldboy36 test\]\# ls \|sed -r 's\#\(^.\*\_\[0-9\]\)\(\_.\*d\)\(.\*$\)\#mv & \1\3\#'

mv stu\_102999\_1\_finished.jpg stu\_102999\_1.jpg

mv stu\_102999\_2\_finished.jpg stu\_102999\_2.jpg

mv stu\_102999\_3\_finished.jpg stu\_102999\_3.jpg

mv stu\_102999\_4\_finished.jpg stu\_102999\_4.jpg

mv stu\_102999\_5\_finished.jpg stu\_102999\_5.jpg

##### 在linux中有专门重命名的命令 rename {#在linux中有专门重命名的命令--rename}

##### rename 被替换的内容 替换的内容 替换的文件（可以使用通配符） {#rename--被替换的内容--替换的内容--替换的文件（可以使用通配符）}

\[root@oldboy tmp\]\# rename "\_finished" "" \*

\[root@oldboy tmp\]\# ls

stu\_102999\_1.jpg stu\_102999\_3.jpg stu\_102999\_5.jpg

stu\_102999\_2.jpg stu\_102999\_4.jpg

\[root@oldboy test\]\# ll

total 0

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_1.jpg

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_2.jpg

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_3.jpg

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_4.jpg

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_5.jpg

\[root@oldboy test\]\# rename jpg JPG \*

\[root@oldboy test\]\# ll

total 0

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_1.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_2.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_3.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_4.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 stu\_102999\_5.JPG

\[root@oldboy test\]\# rename stu oldboy \*

\[root@oldboy test\]\# ll

total 0

-rw-r--r-- 1 root root 0 Sep 2 16:05 oldboy\_102999\_1.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 oldboy\_102999\_2.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 oldboy\_102999\_3.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 oldboy\_102999\_4.JPG

-rw-r--r-- 1 root root 0 Sep 2 16:05 oldboy\_102999\_5.JPG

##### 9）大小写字母相互转换

\[root@iZ25hfz3698Z ~\]\# cat a.txt

a1233\#%bcdefghijklmnopqrstuvwxyz

\[root@iZ25hfz3698Z ~\]\# sed 's\#\[a-z\]\#\u&\#g' a.txt

A1233\#%BCDEFGHIJKLMNOPQRSTUVWXYZ

\[root@iZ25hfz3698Z ~\]\# sed -i 's\#\[a-z\]\#\u&\#g' a.txt

\[root@iZ25hfz3698Z ~\]\# cat a.txt

A1233\#%BCDEFGHIJKLMNOPQRSTUVWXYZ

\[root@iZ25hfz3698Z ~\]\# sed 's\#\[A-Z\]\#\l&\#g' a.txt

a1233\#%bcdefghijklmnopqrstuvwxyz

\[root@oldboy36 ~\]\# tr '\[a-z\]' '\[A-Z\]' &lt; a.txt

A1233\#%BCDEFGHIJKLMNOPQRSTUVWXYZ

echo abcASD \|sed 's\#.\#\u&\#g'

ABCASD

##### 10）一对一字符替换

sed y\#\#\#

cat person.txt

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

sed 'y\#123\#789\#' person.txt

707,oldboy,CEO

708,zhangyao,CTO

709,Alex,COO

704,yy,CFO

705,feixue,CIO

#### 5、查

p命令

\[root@oldboy ~\]\# cat person.txt

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

\[root@oldboy ~\]\# sed -n '1,3p' person.txt

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

#### 6、修改文件

-i 修改文件内容

-i\[备份文件后缀\]

#### 7、Ms \# \# \# Ng 的使用

语法说明：

Ms 第M行处理，无g标志，只处理第一处，有g标志则处理全部

Ng 从第N处开始处理到结尾

Ms 、 Ng 合用 表示 只对第M行从第N处开始处理到结尾

#### 8、数字标志

s \# \# \# N 这种表示替换每行中第N次出现的内容，属于一种精确匹配。

N的取值范围： 1&lt;N&lt;512

cat &gt;num.txt &lt;&lt;EOF

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

EOF

\[root@oldboy ~\]\# cat num.txt

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

\[root@oldboy ~\]\# sed '1s\#1\#0\#1' num.txt

0 1 1 1 1

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

\[root@oldboy ~\]\# sed '1s\#1\#0\#2' num.txt

1 0 1 1 1

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

\[root@oldboy ~\]\# sed '1s\#1\#0\#2g' num.txt

1 0 0 0 0

1 1 1 1 1

1 1 1 1 1

1 1 1 1 1

#### 9、顺序执行多个命令

\[root@oldboy ~\]\# sed -n '3p;5p;10p' /etc/inittab

\# ADDING OTHER CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.

\# System initialization is started by /etc/init/rcS.conf

#### 10、sed参数及符号集合

##### 1）选项 -e

每个 -e 选项后可接一个命令

\[root@oldboy ~\]\# sed -n -e '3p' -e '5p' /etc/inittab

\# ADDING OTHER CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.

\# System initialization is started by /etc/init/rcS.conf

##### 2）选项 -f

\[root@oldboyedu37-nb ~\]\# cat linux36sed.sed

5p

35p

70p

sed -n -f linux36sed.sed linux36sed.txt

##### 3）= 打印行号

\[root@oldboy36 ~\]\# sed -n '$=' person.txt

5

\[root@oldboy32-vm1 ~\]\# sed = nginx.conf \|xargs -n2

1 stu1

2 stu2

3 stu3

4 stu4

5 stu5

6 stu6

7 stu7

8 stu8

9 stu9

10 stu10

##### 4）{ } 里面可以写多个命令

\[root@oldboy ~\]\# sed -n '2,4{=;p}' person.txt

2

102,zhangyao,CTO

3

103,Alex,COO

4

104,yy,CFO

#### 11、模式空间 N

\[root@oldboy ~\]\# cat person.txt

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

\[root@oldboy36 ~\]\# sed 'N;s\#\n\# \#;' person.txt

101,oldboy,CEO 102,zhangyao,CTO

103,Alex,COO 104,yy,CFO

105,feixue,CIO

\[root@oldboy ~\]\# sed "=" person.txt\|sed 'N;s\#\n\# \#g'

1 101,oldboy,CEO

2 102,zhangyao,CTO

3 103,Alex,COO

4 104,yy,CFO

5 105,feixue,CIO

#### 练习题：

1、sed命令执行流程

2、sed的增加：文件的第二行插入一条数据（列要保持对应）

3、sed的删除：删除文件中第三行的数据

4、sed的修改：定位到第四行，将行号109改为193

5、sed的查询：显示第1行到第三行的数据



