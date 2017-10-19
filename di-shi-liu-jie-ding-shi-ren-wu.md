# 第1章 定时任务

### 1.1 什么是crond（定时任务）

通俗讲就是给服务器定了个闹钟

linux系统中用来定期执行命令/脚本或指定程序任务的一种服务或软件

Crond是linux系统中用来定期执行命令／脚本或指定程序任务的一种服务或软件，一般情况下，我们安装完Centos5/6 linux操作系统之后，默认便会启动Crond任务调度服务，在我们前面的系统安装及开机启动优化的设置中，我们也设置保留了Crond开机自启动，Crond服务会定期（默认每分钟检查一次）检查系统中是否有要执行的任务工作，如果有，便会根据其预先设定的定时任务规则自动执行该定时任务工作，这个crond定时任务服务就相当于我们平时早起使用的闹钟一样。

### 1.2 程序、进程、守护进程

1. 程序（文件）：放在磁盘里的，程序代码组成，但是没有在计算机内执行，当前没有执行
2. 进程：所谓进程就是计算机中正则执行/运行的程序，运行起来的程序
3. 守护进程（守护进程）：守护进程就是一直在运行的程序

### 1.3 基础优化的开启自启动服务优化：

\[root@oldboy35-moban ~\]\# chkconfig --list\|egrep "crond\|network\|sshd\|rsyslog\|sysstat"

crond  （定时任务）        	0:off	1:off	2:on	3:on	4:on	5:on	6:off

network  （网络服务）      	0:off	1:off	2:on	3:on	4:on	5:on	6:off

rsyslog  （系统日志服务）      	0:off	1:off	2:on	3:on	4:on	5:on	6:off

sshd    （sshd服务 远程连接服务）   0:off	1:off	2:on	3:on	4:on	5:on	6:off

sysstat        	0:off	1:on	2:on	3:on	4:on	5:on	6:off



服务====&gt;守护进程

	 sshd

### 1.3.1 命令拼接

第一步 开机需要启动的项目

network sshd rsyslog crond sysstat 

#### 1.3.1.1 第一个里程碑-排除你想要保护的

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep "crond\|network\|rsyslog\|sshd\|sysstat"

crond          	0:off	1:off	2:on	3:on	4:on	5:on	6:off

network        	0:off	1:off	2:on	3:on	4:on	5:on 6:off

rsyslog        	0:off	1:off	2:on	3:on	4:on	5:on	6:off

sshd           	0:off	1:off	2:on	3:on	4:on	5:on	6:off

sysstat        	0:off	1:on	2:on	3:on	4:on	5:on	6:off

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep -v "crond\|network\|rsyslog\|sshd\|sysstat"

abrt-ccpp      	0:off	1:off	2:off	3:on	4:off	5:on	6:off

abrtd          	0:off	1:off	2:off	3:on	4:off	5:on	6:off

acpid          	0:off	1:off	2:on	3:on	4:on	5:on	6:off

atd            	0:off	1:off	2:off	3:on	4:on	5:on	6:off

auditd         	0:off	1:off	2:on	3:on	4:on	5:on	6:off

blk-availability	0:off	1:on	2:on	3:on	4:on	5:on	6:off

cpuspeed       	0:off	1:on	2:on	3:on	4:on	5:on	6:off

haldaemon      	0:off	1:off	2:off	3:on	4:on	5:on	6:off

ip6tables      	0:off	1:off	2:on	3:on	4:on	5:on 6:off

iptables       	0:off	1:on	2:off	3:on	4:off	5:off 6:off

irqbalance     	0:off	1:off	2:off	3:on	4:on	5:on	6:off

kdump          	0:off	1:off	2:off	3:on	4:on	5:on	6:off

lvm2-monitor   	0:off	1:on	2:on	3:on	4:on	5:on	6:off

mdmonitor      	0:off	1:off	2:on	3:on	4:on	5:on	6:off

messagebus     	0:off	1:off	2:on	3:on	4:on	5:on	6:off

netconsole     	0:off	1:off	2:off	3:off	4:off	5:off	6:off

netfs          	0:off	1:off	2:off	3:on	4:on	5:on	6:off

nfs-rdma       	0:off	1:off	2:off	3:off	4:off	5:off	6:off

ntpd           	0:off	1:off	2:off	3:off	4:off	5:off	6:off

ntpdate        	0:off	1:off	2:off	3:off	4:off	5:off	6:off

oldboyd        	0:off	1:off	2:off	3:on	4:off	5:on	6:off

postfix        	0:off	1:off	2:on	3:on	4:on	5:on	6:off

psacct         	0:off	1:off	2:off	3:off	4:off	5:off 6:off

quota\_nld      	0:off	1:off	2:off	3:off	4:off	5:off	6:off

rdisc          	0:off	1:off	2:off	3:off	4:off	5:off	6:off

rdma           	0:off	1:off	2:off	3:off	4:off	5:off	6:off

restorecond    	0:off	1:off	2:off	3:off	4:off	5:off	6:off

rngd           	0:off	1:off	2:off	3:off	4:off	5:off	6:off

saslauthd      	0:off	1:off	2:off	3:off	4:off	5:off	6:off

smartd         	0:off	1:off	2:off	3:off	4:off	5:off	6:off

svnserve       	0:off	1:off	2:off	3:off	4:off	5:off	6:off

udev-post      	0:off	1:on	2:on	3:on	4:on	5:on	6:off

#### 1.3.1.2 第二个里程碑-把服务的名字取出来

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep -v "crond\|network\|rsyslog\|sshd\|sysstat"\|awk '{print $1}'

abrt-ccpp

abrtd

acpid

atd

auditd

blk-availability

cpuspeed

haldaemon

ip6tables

iptables

irqbalance

kdump

lvm2-monitor

mdmonitor

messagebus

netconsole

netfs

nfs-rdma

ntpd

ntpdate

oldboyd

postfix

psacct

quota\_nld

rdisc

rdma

restorecond

rngd

saslauthd

smartd

svnserve

udev-post

####  1.3.1.3 第三个里程碑-如何弄出 chkconfig iptables off 

\[root@oldboyedu35-nb ~\]\# echo ipt 

ipt

\[root@oldboyedu35-nb ~\]\# echo ipt \|awk '{print $1}'

ipt

\[root@oldboyedu35-nb ~\]\# echo ipt \|awk '{print "chkconfig"$1}'

chkconfigipt

\[root@oldboyedu35-nb ~\]\# echo ipt \|awk '{print "chkconfig "$1}'

chkconfig ipt

\[root@oldboyedu35-nb ~\]\# echo ipt \|awk '{print "chkconfig "$1"off"}'

chkconfig iptoff

\[root@oldboyedu35-nb ~\]\# echo ipt \|awk '{print "chkconfig "$1" off"}'

chkconfig ipt off

\[root@oldboyedu35-nb ~\]\# \#\#\#拼接出你想要的结果  拼接出你想要的目标

#### 1.3.1.4 第四个里程碑-给找出来的服务-都加上 chkconfig 名字  off 

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep -v "crond\|network\|rsyslog\|sshd\|sysstat"\|awk '{print $1}'

abrt-ccpp

abrtd

acpid

atd

auditd

blk-availability

cpuspeed

haldaemon

ip6tables

iptables

irqbalance

kdump

lvm2-monitor

mdmonitor

messagebus

netconsole

netfs

nfs-rdma

ntpd

ntpdate

oldboyd

postfix

psacct

quota\_nld

rdisc

rdma

restorecond

rngd

saslauthd

smartd

svnserve

udev-post

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep -v "crond\|network\|rsyslog\|sshd\|sysstat"\|awk '{print "chkconfig "$1" off"}'

chkconfig abrt-ccpp off

chkconfig abrtd off

chkconfig acpid off

chkconfig atd off

chkconfig auditd off

chkconfig blk-availability off

chkconfig cpuspeed off

chkconfig haldaemon off

chkconfig ip6tables off

chkconfig iptables off

chkconfig irqbalance off

chkconfig kdump off

chkconfig lvm2-monitor off

chkconfig mdmonitor off

chkconfig messagebus off

chkconfig netconsole off

chkconfig netfs off

chkconfig nfs-rdma off

chkconfig ntpd off

chkconfig ntpdate off

chkconfig oldboyd off

chkconfig postfix off

chkconfig psacct off

chkconfig quota\_nld off

chkconfig rdisc off

chkconfig rdma off

chkconfig restorecond off

chkconfig rngd off

chkconfig saslauthd off

chkconfig smartd off

chkconfig svnserve off

chkconfig udev-post off

#### 1.3.1.5 第五个里程碑-预备知识

\[root@oldboyedu35-nb ~\]\# \#1.PATH 

\[root@oldboyedu35-nb ~\]\# \#2.执行 ---- bash 

\[root@oldboyedu35-nb ~\]\# 

\[root@oldboyedu35-nb ~\]\# 

\[root@oldboyedu35-nb ~\]\# \#\#鸡蛋黄-----linux内核

\[root@oldboyedu35-nb ~\]\# \#\#鸡蛋清-----shell--命令解释器--bash

\[root@oldboyedu35-nb ~\]\# \#\#鸡蛋壳-----命令-软件

\[root@oldboyedu35-nb ~\]\# 

\[root@oldboyedu35-nb ~\]\# echo pwd

pwd

\[root@oldboyedu35-nb ~\]\# echo pwd\|bash

/root

#### 1.3.1.6 第六个里程碑-执行-交给bash执行

\[root@oldboyedu35-nb ~\]\# chkconfig \|egrep -v "crond\|network\|rsyslog\|sshd\|sysstat"\|awk '{print "chkconfig "$1" off"}'\|bash

\[root@oldboyedu35-nb ~\]\# \#\#检查结果

\[root@oldboyedu35-nb ~\]\# chkconfig \|grep 3:on

crond          	0:off	1:off	2:on	3:on	4:on	5:on	6:off

network        	0:off	1:off	2:on	3:on	4:on	5:on 6:off

rsyslog        	0:off	1:off	2:on	3:on	4:on	5:on	6:off

sshd           	0:off	1:off	2:on	3:on	4:on	5:on	6:off

sysstat        	0:off	1:on	2:on	3:on	4:on	5:on	6:off



### 1.3.2 小结

常用服务，必须开机启动的服务crond，sshd，network,rsyslog,sysstat

命令拼接（awk/sed）==&gt;批量==&gt;循环

创造形式（命令）--最后交给bash执行解释



### 1.4 windows定时任务

%windir%\system32\taskschd.msc /s

### 1.5 linux系统crond的定时任务

两种情况

#### 1.5.1 linux系统自身定期执行的任务工作：

系统周期性自行执行的任务工作，如轮循系统日志、备份系统数据、清理系统缓存等，这些任务无需我们认为干预。

\[root@oldboy35-moban ~\]\# ls -l /var/log/messages\*

-rw-------. 1 root root 183394 Mar 31 17:16 /var/log/messages

-rw-------. 1 root root 562454 Mar 21 09:03 /var/log/messages-20170321

-rw-------. 1 root root 131826 Mar 27 09:38 /var/log/messages-20170327

\[root@oldboy35-moban ~\]\# ls -l /var/log/secure\*

-rw-------. 1 root root 7833 Mar 31 11:58 /var/log/secure

-rw-------. 1 root root 6162 Mar 21 09:03 /var/log/secure-20170321

-rw-------. 1 root root 1644 Mar 27 08:35 /var/log/secure-20170327

#### 1.5.2 用户执行的任务工作：某个用户或系统管理员定期要做的任务工作

例如：服务器时间的同步

\[root@oldboyedu35-nb ~\]\# cat /var/spool/cron/root 

cat: /var/spool/cron/root: No such file or directory

\[root@oldboyedu35-nb ~\]\# crontab -l

no crontab for root

1.5.2.1 命令行执行命令--是否好使

\[root@oldboyedu35-nb ~\]\# ntpdate ntp1.aliyun.com

31 Mar 11:02:59 ntpdate\[13433\]: adjust time server 182.92.12.11 offset 0.000046 sec

1.5.2.2 命令要写绝对路径

\[root@oldboyedu35-nb ~\]\# 

\[root@oldboyedu35-nb ~\]\# which ntpdate 

/usr/sbin/ntpdate

\[root@oldboyedu35-nb ~\]\# /usr/sbin/ntpdate  ntp1.aliyun.com

31 Mar 11:03:51 ntpdate\[13440\]: adjust time server 182.92.12.11 offset -0.001770 sec

1.5.2.3命令行测试ok--写入到定时任务中 

\[root@oldboyedu35-nb ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\* \* \* \* \* /usr/sbin/ntpdate  ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\[root@oldboyedu35-nb ~\]\# date -s "1000 day"

Thu Dec 26 11:06:26 CST 2019

\[root@oldboyedu35-nb ~\]\# date 

Thu Dec 26 11:07:04 CST 2019

\[root@oldboyedu35-nb ~\]\# date 

Fri Mar 31 11:07:06 CST 2017

1.5.2.4 修改 每个10分钟

crontab: installing new crontab

\[root@oldboyedu35-nb ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\*/10 \* \* \* \* /usr/sbin/ntpdate  ntp1.aliyun.com &gt;/dev/null 2&gt;&1



1.6 看看是否有定时任务-闹钟-是否能用

1）是否有闹钟

2）是否能用--服务是否启动-正在运行

\[root@oldboyedu35-nb ~\]\# /etc/init.d/crond status

crond \(pid  1498\) is running...

1.7 定时任务Crond使用说明

1.7.1 开机自启动crond服务

\[root@oldboy35-moban ~\]\# chkconfig --list crond

crond          	0:off	1:off	2:on	3:on	4:on	5:on	6:off

1.7.2 此时此刻服务的状态

\[root@oldboyedu35-nb ~\]\# /etc/init.d/crond status

crond \(pid  1498\) is running...

1.7.3 如何查看进程

\[root@oldboy35-moban ~\]\# ps -ef\|grep crond

root       1662      1  0 Mar30 ?        00:00:05 crond

root       5813   3737  0 17:38 pts/0    00:00:00 grep --color=auto crond

1.7.4 小结

1、	crond服务（sshd crond deamon）是运行的程序，而crontab是用来管理用户的定时任务（规则）的命令

2、	crond服务是企业生产工作中常用的重要服务，at和anacron很少用

3、	几乎每个服务器都会用刀crond服务

4、	上千服务器可以开发分布式定时任务项目方案。

1.7.5 指令用法

\[root@oldboy35-moban ~\]\# crontab --help

crontab: invalid option -- '-'

crontab: usage error: unrecognized option

usage:	crontab \[-u user\] file

	crontab \[-u user\] \[ -e \| -l \| -r \]

		\(default operation is replace, per 1003.2\)

	-e	\(edit user's crontab\) 编辑修改 当前用户的定时任务   vi /var/spool/cron/root

	-l	\(list user's crontab\) 查看/显示 当前用户的定时任务 

	-r	\(delete user's crontab\)删除用的定时任务

	-i	\(prompt before deleting user's crontab\) 删除之前提示

	-s	\(selinux context\)

1.7.6 指令选项说明

参数	含义	指定示例

-l （小写字母L）	查看crontab文件内容。提示:l 可理解为list的缩写	crontab -l

-e	编辑crontab文件内容，提示：e可理解为edit的缩写	crontab -e

-i 	删除crontab文件内容，删除前会提示确认。用的很少	crontab -r

-u user	指定使用的用户执行任务

crontab默认编辑当前用户的定时任务配置	crontab -u boy -l

特别强调：-i，-r参数在生产中很少用，没什么需求必须要用-e进去编辑即可，完全是自己的习惯

补充：crontab { -l \| -e } 实际上就是在操作/var/spool/cron/当前用户这样的文件。

使用crontab命令的优点

1、	crontab命令可以检查语法

2、	输入方便

例子：

\[root@oldboy35-moban ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\#\* \* \* \* \* /usr/sbin/ntpdate  ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\#\*/1 \* \* \* \* echo "zzc" &gt;&gt; /server/log/name.log 

\[root@oldboy35-moban ~\]\# ls -l /usr/bin/crontab 

-rwsr-xr-x. 1 root root 51784 Nov 10  2015 /usr/bin/crontab

1.7.7 五个星的解释

通过crontab我们可以用固定的时间间隔执行指定的系统指令或script脚本。时间间隔的单位可以是分、时、日、月、周及以上的任意组合（注意：日和周不要重复，也就是说规定了日就不要在规定周了）。crond服务通过crontab命令可以很容易的实现周期性的日志分析或数据备份等去也运维场景工作。

\[root@oldboy35-moban ~\]\# cat /etc/crontab 

SHELL=/bin/bash

PATH=/sbin:/bin:/usr/sbin:/usr/bin

MAILTO=root

HOME=/



\# For details see man 4 crontabs



\# Example of job definition:

\# .---------------- minute \(0 - 59\)			 					分

  					              时

\# \|  \|  .---------- day of month \(1 - 31\) 						日

\# \|  \|  \|  .------- month \(1 - 12\) OR jan,feb,mar,apr ...                    月

\# \|  \|  \|  \|  .---- day of week \(0 - 6\) \(Sunday=0 or 7\) OR sun,mon,tue,wed,thu,fri,sat 周

\# \|  \|  \|  \|  \|																

\# \*  \*  \*  \*  \* user-name command to be executed

提示：时间记忆口诀：分时日月周。取值范围记忆：正常日期时间范围，小学生都会的了

1.7.8 	时间段的表格

段		含义	取值范围（整数）

第一段	代表分钟	00-59（00或者0）

第二段	代表小时	00-23

第三段	代表日，天	01-31

第四段	代表月份	01-12

第五段	代表星期，周几	0-7（0和7都代表星期日）

分时日月周

1.7.9 crontab 语法格式中特殊符号含义如下表

特殊符号	含义

\*	\*号，表示任意时间都，实际就是“每”的意思

-	减号表示分隔符，表示一个时间范围，区间段，如17-19点，例如：每天的17，18，19点的00分执行任务。00 17-19 \* \* \* cmd

，	逗号，表示分隔时段的意思例如每天的5点10点00分执行任务，00 5,10 \* \* \* cmd

/n	n代表数字，即“每隔n单位时间”，例如：每10分钟执行一次任务可以写成/10 \* \* \* cmd，其中，/10,的范围是0-59，因此也可以写成0-59/10

1.7.10 定时任务的实例

①	 30 3,12 \* \* \* /bin/sh /scripts/oldboy.sh 

每天的凌晨3点或12点 半  执行

②	 30 \*/6 \* \* \* /bin/sh /scripts/oldboy.sh

每6个小时的半点执行 

③	 30 8-18/2 \* \* \* /bin/sh /scripts/oldboy.sh

     早上8点到18点每隔2个小时 的半点执行 脚本 

     8,9,10,11,12,13,14,15,16,17,18

     30 8,10,12,14,16,18 \* \* \*  /bin/sh /scripts/oldboy.sh     

④	 30 21 \* \* \* /application/apache/bin/apachectl graceful

     每天的21点30分执行 重启apache软件

⑤	 45 4 1,10,22 \* \* /application/apache/bin/apachectl graceful

     每个月1,10,22号 凌晨4点45分 重启apache软件

⑥	 10 1 \* \* 6,0 /application/apache/bin/apachectl graceful

     周六 周日的 凌晨1点10分  重启apache软件

⑦	 0,30 18-23 \* \* \* /application/apache/bin/apachectl graceful

     18到23点 整点和半点执行  重启apache软件

     0,30 18,19,20,21,22,23 重启apache软件

⑧	 00 \*/1 \* \* \* /application/apache/bin/apachectl graceful

     00 \* \* \* \* /application/apache/bin/apachectl graceful

⑨	 \* 23,00-07/1 \* \* \* /application/apache/bin/apachectl graceful

     \* 23 \* \* \* \* /application/apache/bin/apachectl graceful

     00 23,00-07/1 \* \* \* /application/apache/bin/apachectl graceful

01 \* \* \* \* cmd \#每小时的01分钟执行

字面意思上是什么时间

然后在想多久执行一次

02 04 \* \* \* cmd \#每天4点的02分钟执行

22 14 \* \* 00 cmd \#每周日的14点22分执行

42 04 01 \* \* cmd \#每月1日的4点42分执行

1.7.11 小结

提示：

1，cmd为要执行的命令或脚本，例如：/bin/sh /server/scripts/chensiqi.sh

2,每个列之间必须要有一个空格。多个空格可以么？自己实践

3,第一个里程碑：把字面的翻译成实际的时间（这里不用考虑多久一次/重复）

4,第二个里程碑：思考多久重复一次或者思考下一次执行是什么时候

`强调：周和日不能同时使用`

1.7.12 实例 打印自己的名字

\#\#\#第一个里程碑-准备环境

\[root@oldboy35-moban ~\]\# mkdir -p  /server/log 

\#\#\#第二个里程碑-命令试试

\[root@oldboy35-moban ~\]\# echo zhaozhichao &gt;&gt;/server/log/name.log

\[root@oldboy35-moban ~\]\# cat /server/log/name.log

zhaozhichao 

\#\#\#第三个里程碑-写入到定时任务

\[root@oldboyedu35-nb ~\]\# 

\[root@oldboy35-moban ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\* \* \* \* \* /usr/sbin/ntpdate  ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\*/1 \* \* \* \* echo "zhaozhichao" &gt;&gt; /server/log/name.log 

\#\#\#第四个里程碑-查看-检查

\[root@oldboy35-moban ~\]\# tail -f /server/log/name.log 

zhaozhichao

zhaozhichao





1.8 总结：

1、定时任务要加注释

2、如果已经要定向到文件（把命令或脚本的结果放到文件）中，结尾不要有&gt;/dev/null 2&gt;&1

3、/server/log 目录必须要存在才能出结果，如没有创建这个目录

4、定时任务中的路径一定要绝对路径

5、crond服务必须首先开启

6、查看定时任务日志 tail /var/log/cron



1.9 定时任务书写要领

1.9.1 要领1：为定时任务规则加必要的注释

1.9.2 要领2：执行shell脚本任务前加/bin/sh

1.9.3 要领3：定时任务命令或脚本的结尾加&gt;/dev/null 2&gt;&1 或定向到一个文件

1.9.4 要领4：定时任务命令超过2条的命令执行，最好用脚本文件

定时任务写法：

\* \* \* \* \* /bin/sh /server/scripts/log.sh &gt;dev/null 2&gt;&1

定时任务：给定时任务看病的日志 /var/log/cron

技巧:

1\)	命令程序要用绝对路径

2\)	脚本中用到系统的环境变量要重新定义

3）crontab定时任务的10个生产基本要领和调试技巧，尤其是要学会看服务日志来调试。

4）生产环境使用crontab定时任务要注意的10点箴言。

1.9.5 【企业案例】如果定时任务规则结尾不加&gt;/dev/null 2&gt;&1 或者追加到文件中

&gt;&gt;/tmp/oldboy  2&gt;&1，很容易导致硬盘inode空间被占满，从而系统服务不正常

解决方法：

删除大量的小文件/var/spool/postfixdrop/ 下所有的文件

ls \|xargs rm

删除上级目录（看好目录的属性（所有者 组 权限））

临时开启postfix（sendmail）服务（工作中）

1.9.6 磁盘不足系列的解决方法

inode满了----定时任务 没有定向到空或文件

block满了

文件硬链接数为0，但是进程占用，所有没有被释放，会越来越多 block

磁盘空间满了：

1.	inode满了 df -i

2.	block 正常的满了 df -h

du -sh /\*

du -sh /usr/\*

3.	block 非正常的满了 df -h  

du -sh /\*  文件的硬链接数为0，但是还有进程调用。

lsof \|grep delete





1.7.6 要领5：在指定用户下执行相关定时任务

1.7.7 要领6：生产任务程序不要随意打印输出信息

1、	定向到文件

2、	&gt;/dev/null 2&gt;&1

1.7.8 要领7：定时任务执行的脚本要规范路径

1.7.9 要领8：配置定时任务规范操作过程，防止出错（复制，粘贴）

1.7.10 小结：

1、	为定时任务规则加必要的注释

2、	执行shell脚本任务前加/bin/sh

3、	定时任务命令或脚本结尾加&gt; 文件路径 或 &gt;/dev/null 2&gt;&1

4、	定时任务命令或程序最好写到脚本里执行

5、	在指定用户下执行相关的定时任务

6、	生产任务程序不要随意打印输出信息

7、	定时任务执行的脚本要规范路径（/server/scripts）

8、	配置定时任务规范操作过程





1.8 crontab 定时任务生产应用问题10箴言

1.8.1 需要修改系统环境变量问题

export PATH

1.命令的绝对路径

2.在脚本中，修改使用的PATH

export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

1.8.2 定时任务要用绝对路径

1.8.3 定时任务的脚本权限问题

/bin/sh shell的脚本

1.8.4 时间变量问题用反斜线

cd /&& tar zcf /data/html\_$\(date +\%F-\%M-\%H-%S\).tar.gz var/www/

1.8.5 定时任务里面的命令或脚本要定向到空或指定个文件

/dev/null 2&gt;&1 或者 &gt;&gt; /server/log/ip.log 2&gt;&1

1.8.6 定时任务规则之前加注释

1.8.7 使用脚本程序替代命令行定时任务

1.8.8 避免不必要的程序及命令输出

1.8.9 打包压缩使用相对路径（切到目录目录的上一级打包目标）

1.8.10 定时任务脚本中的程序命令及路径尽量用全路径

1.9 定时任务使用命令出现的报错

常见报错

command not found 命令没有找到

No such file or directory 没有这个文件或目录

Permission denied 权限不足

1.10 定时任务步骤

\#\#\#\#第一个里程碑-准备环境

mkdir

\#\#\#\#第二个里程碑-命令行执行命令--是否好使

tar 或者

升级版

cd / && tar 放包目录.tar.gz  要打包的目录

\#\#\#\#第三个里程碑-放入到脚本（文件）  xxxx.sh 

/bin/sh xxx.sh

\#\#\#\#第四个里程碑-写入到定时任务里面

\* \* \* \* \* /bin/sh xxx.sh /dev/null 2&gt;&1

升级版

写真正的定时任务

\#\#\#\#第五个里程碑-检查并修改定时任务执行时间

tail -f /var/log/cron

ls 目录



