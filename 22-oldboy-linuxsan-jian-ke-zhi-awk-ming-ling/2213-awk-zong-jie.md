awk工作原理

13.2 BEGIN 与 END

BEGIN模块输出一些提示性文字 awk内置变量FS,RS,ORS,OFS

END模块输出一些提示性文字，显示最后的结果，计算空行，awk数组，取苹果的过程把苹果

展示处理

awk里面的普通变量不用初始化

awk先处理，一行一行处理，然后END模块输出

13.3 域、记录

FS 指定各种各样的刀（正则表示），RS 正则表示

13.4 模式匹配 ===&gt; 条件

正则表达式

^ 字符串开头

$ 字符串结尾

$3~/^https/

--posix 或 --re-interval

NR==1

NR&gt;=2

模式默认匹配 一行 $0

$3~/^r/

/reg/ 默认匹配整行 $0

awk '$3~/\[4-6\]/{print $0}'

范围匹配

NR==2，NR==5 ====&gt; 2,5p

/start位置/,/结束位置/

显示Dan第二次捐款金额

显示TOM的名字和电话号码

显示所有以138开头的号码的人的全名和手机号码

显示所有以一个C或E开头的人名

显示所有手机号码最后数字是1或5的人名

显示Chet的捐款.每个值时都有以$开头.如$520$200$135

显示姓,其后跟一个逗号和名,如Jody,Savage

\[root@db02 files\]\# cat reg.txt

Mike Harrington: 13716352255 :250:100:175

Christian Dobbins: 13901284715 :155:90:201

Susan Dalsass: 13810756741 :250:60:50

Nancy McNeil: 13810862484 :250:80:75

John Goldenrod: 13521156269 :250:100:175

Chet Main: 13810733714 :50:95:135

Tom Savage: 13716052112 :250:168:200

Elizabeth Stachelin: 18811233838 :175:75:300

Archie McNichol: 13520593076 :250:100:175

Jody Savage: 13716802727 :15:188:150

Guy Quigley: 13520321021 :250:100:175

Dan Savage: 13716375331 :450:300:275

\[root@db02 files\]\# awk -F "\[ :\]+" '$1~/Dan/{print $\(NF-1\)}' reg.txt

300

\[root@db02 files\]\# awk -F "\[ :\]+" '$1~/Tom/{print $1,$3}' reg.txt

Tom 13716052112

\[root@db02 files\]\# awk -F "\[ :\]+" '$3~/^138/{print $1,$2,$3}' reg.txt

Susan Dalsass 13810756741

Nancy McNeil 13810862484

Chet Main 13810733714

\[root@db02 files\]\# awk '$1~/^\(C\|E\)/{print $1}' reg.txt

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

13.5 轻松精通awk数组企业问题案例

[http://oldboy.blog.51cto.com/2561410/1687026](http://oldboy.blog.51cto.com/2561410/1687026)

\[root@show test\_2016-05-11\]\# cat pro1.txt

a 1

b 2

c 3

d 5

a 3

c 4

c 9

d 1

awk '{kuang\[$1\]+=$2}END{for\(shou in kuang\)print shou,kuang\[shou\]}' pro1.txt

a 4

b 2

c 16

d 6

\[root@db02 files\]\# cat add.txt

a 1

b 3

c 2

d 7

b 5

a 3

g 2

f 6

d 9

\[root@db02 files\]\# awk '{a\[$1\]+=$2}END{for\(i in a\)print i,a\[i\]}' add.txt

a 4

b 8

c 2

d 16

f 6

g 2

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{print $0}' pro3.txt

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

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++;print $1,kuang\[$1\]}' pro3.txt

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

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++;print $1"\t"kuang\[$1\]}' pro3.txt

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

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++}END{for\(shou in kuang\)print shou,kuang\[shou\]}' pro3.txt

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

\[root@show test\_2016-05-11\]\# awk 'BEGIN{RS="\[ \n\]"}{kuang\[$1\]++}END{for\(shou in kuang\)print shou,kuang\[shou\]}' pro3.txt \| sort -rnk2

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

13.6 awk 二维数组

awk '{s\_num\[$1,$7\]++;s\_size\[$1,$7\]+=$10}{for\( i in s\_num\)split\(i,idx,SUBSEP\);{print s\_num\[idx\[1\],idx\[2\]\],idx\[1\],idx\[2\],s\_size\[idx\[1\],idx\[2\]\]}}' access1.log

第14章 附

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

```
{if\($i~/^id=.\*$/\){a=$i};

 if\($i~/^\[a-z\]{2}$/\){b=$i};

if\($i~/^\[a-z\]{4}$/\){c=$i};

if\($i~/^name=.\*$/\){d=$i}};

print a,b,d,c}'

```

file.txt \|sort\|uniq

awk打印99乘法表

\[root@oldboy36 ~\]\# awk 'BEGIN{for\(x=1;x&lt;=9;x++\){for\(i=1;i&lt;=x;i++\){printf i"x"x"="i\*x" "}print}}' \|column -t

1x1=1

1x2=2 2x2=4

1x3=3 2x3=6 3x3=9

1x4=4 2x4=8 3x4=12 4x4=16

1x5=5 2x5=10 3x5=15 4x5=20 5x5=25

1x6=6 2x6=12 3x6=18 4x6=24 5x6=30 6x6=36

1x7=7 2x7=14 3x7=21 4x7=28 5x7=35 6x7=42 7x7=49

1x8=8 2x8=16 3x8=24 4x8=32 5x8=40 6x8=48 7x8=56 8x8=64

1x9=9 2x9=18 3x9=27 4x9=36 5x9=45 6x9=54 7x9=63 8x9=72 9x9=81

学习正则表达式，一定要通过

grep或egrep学习 配合 egrep -o

alias grep='grep --color=auto'

alias egrep='egrep --color=auto'

awk调试工具 pgawk

