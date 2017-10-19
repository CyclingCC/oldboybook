第一章 第三关命令

1.1 请执行命令取出linux中eth0的IP地址\(请用cut，有能力者也可分别用awk,sed命令答\)。

方法1

ifconfig eth0 \|sed -n '2p'\|cut -d ":" -f2 \|cut -d " " -f1

方法2

ifconfig eth0\|awk -F "\[ :\]+" 'NR==2{print $4}'

方法3

ifconfig eth0\|sed -n 's\#^.\*ddr:\#\#gp'\|sed -n 's\#B.\*$\#\#gp'

方法4

ifconfig eth0 \|sed -nr '2s\#^.\*dr:\(.\*\)  Bc.\*$\#\1\#gp'

ifconfig eth0\|sed -rn '2s\#^\[^0-9\]+\(.\*\)  Bc.\*$\#\1\#p'

方法5

ifconfig eth0\|grep -Eo "\(\[0-9\]{1,3}\.\){3}\[0-9\]{1,3}" \|head -1 

方法6

ifconfig eth0 \|grep -Po '\(?&lt;=addr:\)\S+'





处理技巧：

	匹配需要的目标\(获取的字符串如ip\)前的字符串一般用以.....开头（^.\*）来匹配开头，匹配的结尾写上实际的字符，如："^.\*addr:"    表示匹配  “			inet addr:”

而处理需要的目标后的内容一般在匹配的开头写上实际的字符，而结尾是用以.......结尾\(.\*$\)来匹配

如:   Bcast:.\*$    表示匹配  “Bcast:10.0.0.25  Mask:255.255.255.0”



1.2  如何取得/etiantian文件的权限对应的数字内容，如-rw-r--r--为644，要求使用命令取得644这样的数字。

\[root@oldboy test\]\# stat /etiantian\|sed -nr 's\#^.\*\\(0\(.\*\)/-.\*$\#\1\#gp'

644

\[root@oldboy test\]\# stat /etiantian \|awk -F "\[0/\]" 'NR==4{print $2}'

644

\[root@oldboy36 test\]\# stat -c %a /etiantian

644

-oldboy-

1.2.1 方法1：

\[root@oldboy ~\]\# touch /etiantian 

\[root@oldboy ~\]\# ls -lhi /etiantian 

2318 -rw-r--r-- 1 root root 0 4月   3 09:58 /etiantian

\[root@oldboy ~\]\# ls -l /etiantian \|cut -c 2-10\|tr "rwx-" "4210"

420400400

\[root@oldboy ~\]\# ls -l /etiantian \|cut -c 2-10\|tr "rwx-" "4210"\|awk -F "" '{print $1+$2+$3""$4+$5+$6""$7+$8+$9}'

644

1.2.2  方法2：

\[root@oldboy ~\]\# stat /etiantian \|sed -rn '4s\#^.\*\\(0\(.\*\)/-.\*$\#\1\#gp'

644

1.2.3 方法3：

\[root@oldboy ~\]\# stat -c %a /etiantian 

644

1.2.4 方法4

\[root@oldboy ~\]\# stat /etiantian \|awk -F "\[0/\]" 'NR==4{print $2}'   

644

1.2.5 方法5：

\[root@oldboy ~\]\# stat /etiantian \|sed -n '4p'\|egrep -o "\[1-9\]{3}"

644

curl     -s  不显示错误信息

	  	 -I   取协议（http/ftp等）头

\[root@oldboy ~\]\# curl -I www.baidu.com 2&gt;/dev/null \|sed -n '1p'

HTTP/1.1 200 OK

\[root@oldboy ~\]\# curl -s -I www.baidu.com \|sed -n '1p'

HTTP/1.1 200 OK

1.3  查找当前目录下所有文件，并把文件中的www.etiantian.org字符串替换成www.oldboy.cc

\[root@xdz test\]\# mkdir a/{b,c/d} -pv

mkdir: created directory \`a'

mkdir: created directory \`a/b'

mkdir: created directory \`a/c'

mkdir: created directory \`a/c/d'

\[root@xdz test\]\# tree

.

├── a

│   ├── b

│   └── c

│       └── d

└── oldboy.log



4 directories, 1 file

\[root@xdz test\]\# touch a/aa.txt a/b/bb.txt a/c/cc.txt a/c/d/dd.txt

\[root@xdz test\]\# tree

.

├── a

│   ├── aa.txt

│   ├── b

│   │   └── bb.txt

│   └── c

│       ├── cc.txt

│       └── d

│           └── dd.txt

└── oldboy.log



4 directories, 5 files

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/aa.txt 

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/b/bb.txt 

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/c/cc.txt 

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/c/d/dd.txt 





方法1:

find  +  \|xargs sed

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f \|xargs cat 

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f \|xargs sed 's\#www.etiantian.org\#www.oldboy.cc\#'

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc

方法2：

find  +  -exec sed

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f -exec cat {} \;

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f -exec sed 's\#www.etiantian.org\#www.oldboy.cc\#' {} \;

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc

方法3：

sed  +  $\(\)

\[root@oldboy36 oldboy\]\# cat $\(find /oldboy/ -type f\)

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# sed 's\#www.etiantian.org\#www.oldboy.cc\#' $\(find /oldboy/ -type f\)

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc





1.4  linux下通过mkdir命令创建一个新目录/oldboy/ett，它的硬链接数是多少，为什么？如果在/oldboy/ett下面再创建一个目录test。再问/oldboy/ett的硬链接数是多少？为什么

\[root@oldboy ~\]\# ls -ld /oldboy/ett/

drwxr-xr-x 2 root root 4096 4月   3 09:35 /oldboy/ett/

硬链接数为2

因为：

1、创建目录本身为一个硬链接

2、ett下隐藏目录.\(点\)为ett目录的又一个硬链接

3、ett下test目录下隐藏文件..\(点点\)也是ett目录的一个硬链接

\[root@oldboy oldboy\]\# ls -ld /oldboy/ett/

drwxr-xr-x 3 root root 4096 Apr  3 11:31 /oldboy/ett/



1.5  请问在一个命令上加什么参数可以实现下面命令的内容在同一行输出。

echo "oldboy";echo "oldboy"

\[root@xdz test\]\# echo -n "oldboy";echo "oldboy"

oldboyoldboy

1.6  已知/oldboy/ett.txt文件内容为：

oldboy

olldboooy

test

请使用grep或egrep正则匹配的方式过滤出前两行内容

\[root@oldboy ~\]\# grep -v "^$" ett.txt    

oldboy

xizi

xiaochao

\[root@oldboy ~\]\# sed "/^$/d" ett.txt              

oldboy

xizi

xiaochao

\[oldboy@oldboy ~\]$ cat a.txt

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# cat ett.txt 

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# grep -v "^o" ett.txt   \#→排除以o开头的内容

test

\[root@oldboy oldboy\]\# grep "^o" ett.txt      \#→过滤以o开头的内容

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "y$" ett.txt      \#→排除以y结尾的内容

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol." ett.txt      \#→.代表任意字符

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol.\*" ett.txt   \#→\*表表示重复前一个字符1次或多次，.\*结合匹配所有字符。

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\{0,1\}" ett.txt  \#→重复前一个字符0-1次

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\{5,6\}" ett.txt \#→重复前一个字符l,5-6次

\[root@oldboy oldboy\]\# grep "ol\{0\}" ett.txt \#→重复前一个字符l,正好0次

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\[db,ldboo\]" ett.txt 

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\[dbldboo\]" ett.txt 

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "\[^test\]" ett.txt \#→过滤出不包含test的内容，此处^和以。。。开头不同。

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "\[^t\]" ett.txt 

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# grep "^\[^t\]" ett.txt \#→过滤出不以t开头的内容

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.bo...y' a.txt 

\[oldboy@oldboy ~\]$ grep 'ol.bo\*y' a.txt 

oldboy

\[oldboy@oldboy ~\]$ grep 'bo\*y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo.\*y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo...y' a.txt 

\[oldboy@oldboy ~\]$ grep 'bo\{2,3\}y' a.txt 

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo\{1,3\}y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol\{1,2\}dbo\{1,3\}y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo\*y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo.\*y' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.\*d' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.d' a.txt 

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol+d' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol?d' a.txt 

oldboy

\[oldboy@oldboy ~\]$ egrep 'ol+?d' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)y' a.txt 

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)oy' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ echo ollldboooooy &gt;&gt;a.txt 

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)oy' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)\*oy' a.txt 

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol?d' a.txt 

oldboy

\[oldboy@oldboy ~\]$ egrep 'ol+d' a.txt 

oldboy

olldboooy

ollldboooooy

\[root@oldboy /data\]\# egrep "ol+dbo+y"  /oldboy/ett.txt  

oldboy

olldboooy

\[root@oldboy /data\]\# sed -n '/ol+dbo+y/p' /oldboy/ett.txt

\[root@oldboy /data\]\# sed -nr '/ol+dbo+y/p' /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# awk '/ol+dbo+y/'  /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# egrep "ol+dbo+y"  /oldboy/ett.txt  

oldboy

olldboooy

\[root@oldboy /data\]\# sed -nr '/ol+dbo+y/p' /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# awk '/ol+dbo+y/'  /oldboy/ett.txt

oldboy

olldboooy

1.7  date命令

\[root@oldboy ~\]\# LANG=en

\[root@oldboy ~\]\# date   

Mon Mar 21 08:36:28 CST 2016

\[root@oldboy ~\]\# 

\[root@oldboy ~\]\# 

\[root@oldboy ~\]\# 

\[root@oldboy ~\]\# date -s "2016/05/01"

Sun May  1 00:00:00 CST 2016

\[root@oldboy ~\]\# date

Sun May  1 00:00:02 CST 2016

\[root@oldboy ~\]\# date -s "20160501"  

Sun May  1 00:00:00 CST 2016

\[root@oldboy ~\]\# date -s "20160501 11:45:00"

Sun May  1 11:45:00 CST 2016

\[root@oldboy ~\]\# date -s "20160502 11:45:00"

Mon May  2 11:45:00 CST 2016

\[root@oldboy ~\]\# date -s "05/05/2016"

Thu May  5 00:00:00 CST 2016

\[root@oldboy ~\]\# hwclock -w



1.8  请给出如下格式的date命令例：11-02-26。在给出实现按周输出比如：周六输出为6，请分别给出命令

\[root@oldboy oldboy\]\# date +%F

2016-04-03

\[root@oldboy oldboy\]\# date +%Y-%m-%d\ %H:%M:%S

2016-04-03 11:50:24

 \[root@oldboy oldboy\]\# date +%F\ %T

2016-04-03 11:50:45

\[root@oldboy oldboy\]\# date +%w

0

显示其他时间：

\[root@oldboy ~\]\# date +%F

2016-04-03

\[root@oldboy ~\]\# date +%F -d "-2day"

2016-04-01

\[root@oldboy ~\]\# date +%F -d "+2day"

2016-04-05

\[root@oldboy ~\]\# date +%F -d "+48Hour"

2016-04-05

\[root@oldboy ~\]\# date +%F -d "+1440Min"

2016-04-04



\[root@oldboy ~\]\# tar zcvf oldboy\_$\(date +%F\).tar.gz ./oldboy/

00:00:00切割，改名

mv oldboy\_$\(date +%w -d "-1day"\).tar.gz oldboy\_$\(date +%F -d "-1day"\).tar.gz

1.9  当从root用户切到普通用户时，执行ifconfig会提示。

\[oldboy@student ~\]$ ifconfig -bash: ifconfig: command not found   

提示：c58会遇到，c64没有此问题。  请问这是为什么？如何解决，请给出详细解决过程

PATH  环境变量中没有ifconfig命令的路径

\[root@xdz ~\]\# which ifconfig

/sbin/ifconfig

echo  ' PATH=$ PATH: /sbin/ifconfig '  &gt;&gt;  ~/.bash\_profile

.  ~/.bash\_profile



1.10  请描述下列路径的内容是做什么的？

/var/log/messages          系统日志

/var/log/secure				系统安全日志

/var/spool/clientmqueue		邮件临时目录

/proc/interrupts			查看中断文件

/etc/fstab					磁盘文件系统开机自动挂载文件

/etc/profile 				全局的环境配置文件



1.11  如何快速查到ifconfig的全路径（假如你不知道其路径），请给出命令。

which

\[root@oldboy36 ~\]\# which ifconfig

/sbin/ifconfig

locate

\[root@oldboy36 ~\]\# locate ifconfig

/sbin/ifconfig

/usr/sbin/pifconfig

/usr/share/man/de/man8/ifconfig.8.gz

/usr/share/man/fr/man8/ifconfig.8.gz

/usr/share/man/man8/ifconfig.8.gz

/usr/share/man/man8/pifconfig.8.gz

/usr/share/man/pt/man8/ifconfig.8.gz

whereis

\[root@oldboy36 ~\]\# whereis ifconfig

ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz

find查找

\[root@oldboy36 ~\]\# find /sbin/ /usr/sbin/ /usr/local/sbin/ -type f -name "ifconfig"

/sbin/ifconfig



1.12  请给出正确的关机和重起服务器的命令

关机

shutdown -h now    \# 立刻关机

shutdown -h 1      \#1分钟以后关机

halt              \# 立即停止系统，需要人工关闭电源

init 0

poweroff        \# 立即停止系统，并且关闭电源

重启

shutdown -r now

reboot

init 6



1.13  命令行快捷键命令的功能

光标移动

Ctrl + a 切换到命令行开始

Ctrl + e 切换到命令行末尾

剪切粘贴

Ctrl + u 清除（剪切）光标之前的内容

Ctrl + k 清除（剪切）光标之后的内容

ctrl + y 粘贴

esc + f 把光标移动到单词的结尾

esc + b 把光标移动到单词的开头

ctrl + b  光标向左移动一个符号的位置

ctrl + f  光标向右移动一个符号的位置

命令查询

Ctrl + r查找（历史命令）。 history\|grep 

ctrl + p  previous ↑上一个命令

ctrl + n  next    ↓下一个命令

其他类型

Ctrl + c 终止当前命令或脚本           

Ctrl + d 退出当前shell，相当于exit logout，一个个删除光标后字符。

Ctrl + l 清除屏幕内容，相当于clear。

tab 所有命令及路径补全功能，一般要多按几下

esc + .   引用/使用上一个命令的最后一个参数（结尾）

SecureCRT快捷键

Ctrl+shift+c 命令行复制内容  

Ctrl+shift+v 命令行粘贴内容

Xshell快捷键

Shift+insert 粘贴

Ctrl+insert 复制



