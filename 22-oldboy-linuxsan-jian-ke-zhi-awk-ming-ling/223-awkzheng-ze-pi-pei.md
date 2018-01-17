$1~/……/ $1正则匹配

$3~/……/ $3正则匹配

$4!~/....../ $4正则不匹配

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

\#\#\#\#\#\#\#\#

#### 3.1 awk正则表达式练习题

测试环境

mkdir -p /server/files/

cat &gt;&gt;/server/files/reg.txt&lt;&lt;EOF

Zhang Dandan 41117397 :250:100:175

Zhang Xiaoyu 390320151 :155:90:201

Meng Feixue 80042789 :250:60:50

Wu Waiwai 70271111 :250:80:75

Liu Bingbing 41117483 :250:100:175

Wang Xiaoai 3515064655 :50:95:135

Zi Gege 1986787350 :250:168:200

Li Youjiu 918391635 :175:75:300

Lao Nanhai 918391635 :250:100:175

EOF

##### 3.1.1 显示姓zhang的人的第二次捐款金额及他的名字

\[root@oldboy files\]\# awk -F '\[ :\]+' '$1~/Zhang/{print $2,$5}' reg.txt

Dandan 100

Xiaoyu 90

##### 3.1.2 显示xiaoyu的姓和id号

\[root@oldboy files\]\# awk -F '\[ :\]+' '$2~/Xiaoyu/{print $1,$3}' reg.txt

Zhang 390320151

##### 3.1.3 显示所有以41开头的id号的人的全名和id号

\[root@oldboy files\]\# awk -F '\[ :\]+' '$3~/^41.\*/{print $1,$2,$3}' reg.txt

Zhang Dandan 41117397

Liu Bingbing 41117483

##### 3.1.4 显示所有以一个D或X开头的人名全名

\[root@oldboy files\]\# awk -F '\[ :\]+' '$2~/^\(D\|X\)/{print $1,$2}' reg.txt

Zhang Dandan

Zhang Xiaoyu

Wang Xiaoai

##### 3.1.5 显示所有id号最后一位数字是1或5的人的全名

\[root@oldboy files\]\# awk -F '\[ :\]+' '$3~/\(1\|5\)$/{print $1,$2}' reg.txt

Zhang Xiaoyu

Wu Waiwai

Wang Xiaoai

Li Youjiu

Lao Nanhai

##### 3.1.6 显示xiaoyu的捐款，每个值都以$开头，如$520$200$135

\[root@oldboy files\]\# awk -F '\[ :\]+' 'BEGIN{OFS="$"}$2~/Xiaoyu/{print "$"$4,$5,$6}' reg.txt

$155$90$201

##### 3.1.7 显示所有人的全名，以姓，名的格式显示，如Meng,Feixue

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

#### 3.2 awk中替换函数

gsub\(/正则匹配/,"替换后的内容",字段\)

\[root@oldboy files\]\# awk '$2~/^Xiaoyu$/{gsub\(/:/,"$",$NF\);print $NF}' reg.txt

$155$90$201

#### 3.3 重要思想

正则表达式如何学好 sed ， awk ， grep

通过egrep查看大致结果

通过egrep -o查看到底匹配了什么

取ip

\[root@nfsserver files\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2{print $4}'

10.0.0.31

\[root@nfsserver files\]\# ifconfig eth0\|awk -F "\(addr:\)\|\( Bcast:\)" 'NR==2{print $2}'

10.0.0.31

取反思想

\[root@oldboy files\]\# ifconfig eth0 \|awk -F '\[^0-9.\]+' 'NR==2{print $2}'

10.0.0.10

#### 3.4 awk支持{}的方法

--posix 或 --re-interval 使用{}时，使用

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

