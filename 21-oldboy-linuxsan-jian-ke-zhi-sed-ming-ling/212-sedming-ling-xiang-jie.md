##  2.1 创建环境 {#21--创建环境}

cat &gt;person.txt&lt;&lt;EOF

101,oldboy,CEO

102,zhangyao,CTO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

EOF

## 2.2 增 {#22--增}

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

## 2.3 多行增 {#23--多行增}

\[root@oldboy ~\]\# echo -e "oldboy\noldboy"

oldboy

oldboy

## 企业案例1：优化SSH配置（一键完成增加若干参数） {#企业案例1：优化ssh配置（一键完成增加若干参数）}

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

## 2.4 { } 作用 {#24----作用}

![](https://www.luffycity.com/linux-book/assets/20-3.png)

## 2.5 调试工具sedsed命令 {#25--调试工具sedsed命令}

安装sedsed命令

wget[http://sedsed.sourceforge.net/sedsed-1.0](http://sedsed.sourceforge.net/sedsed-1.0)-O /bin/sedsed

PATT是pattern模式的缩写，即模式空间

HOLD是保持空间

COMM是command的缩写，即sed命令

sedsed -d --hide=hold "2i 106,dandan,CSO" person.txt

## 2.6 删 {#26--删}

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

## 2.7 地址范围 {#27--地址范围}

sed软件可以对单行或多行文本进行处理。如果在sed命令前面不指定地址范围，那么默认会匹配所有行

用法： n1\[,n2\]{sed-commands}

地址用逗号分隔，n1,n2 可以用数字、正则表达式、或者二者的组合表示

![](https://www.luffycity.com/linux-book/assets/tab20-7.png)

## 2.8 改 {#28--改}

### 2.8.1 按行替换 {#281--按行替换}

c 用新行取代旧行 c change

\[root@oldboy ~\]\# sed '2c 106,dandan,CSO' person.txt

101,oldboy,CEO

106,dandan,CSO

103,Alex,COO

104,yy,CFO

105,feixue,CIO

### 2.8.2 字符串替换 {#282--字符串替换}

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

### 2.8.3 使用s命令替换为空 {#283--使用s命令替换为空}

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

### 2.8.4 变量替换 {#284--变量替换}

\[root@oldboy ~\]\# cat test.txt

a

b

a

\[root@oldboy ~\]\# x=a;y=b

\[root@oldboy ~\]\# sed "s\#$y\#$x\#" test.txt

a

a

a

### 2.8.5 特殊命令 eval {#285--特殊命令-eval}

\[root@oldboy ~\]\# eval sed 's\#$y\#$x\#' test.txt

a

a

a

### 2.8.6 分组替换 {#286--分组替换}

sed软件的\\(\\)的功能可以记住正则表达式的一部分，其中， \1为第一个记住的模式

即第一个小括号中匹配的内容， \2为第二个记住的模式，即第二个小括号中匹配的内容，

sed最多可以记住9个

关闭开机自启动的服务

chkconfig --list \|grep "3:on"\|egrep -v "sshd\|crond\|network\|rsyslog\|sysstat"\|awk '{print $1}'\|sed -r 's\#\(^.\*\)\#chkconfig \1 off\#g'\|bash

### 2.8.7 sed软件s命令中的特殊符号& {#287--sed软件s命令中的特殊符号}

&代表s\#\#\#g 中前两个\# 之间的全部内容

### 2.8.8 批量修改文件名 {#288--批量修改文件名}

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

### 2.8.9 大小写字母相互转换 {#289--大小写字母相互转换}

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

### 2.8.10 一对一字符替换 {#2810--一对一字符替换}

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

## 2.9 查 {#29--查}

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

## 2.10 修改文件 {#210--修改文件}

-i 修改文件内容

-i\[备份文件后缀\]

