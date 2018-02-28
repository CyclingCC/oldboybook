#### 1、开机自启动crond服务 {#171-开机自启动crond服务}

\[root@oldboy35-moban ~\]\# chkconfig --list crond

crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off

#### 2、此时此刻服务的状态 {#172-此时此刻服务的状态}

\[root@oldboyedu35-nb ~\]\# /etc/init.d/crond status

crond \(pid 1498\) is running...

#### 3、如何查看进程 {#173-如何查看进程}

\[root@oldboy35-moban ~\]\# ps -ef\|grep crond

root 1662 1 0 Mar30 ? 00:00:05 crond

root 5813 3737 0 17:38 pts/0 00:00:00 grep --color=auto crond

#### 4、小结 {#174-小结}

1）crond服务（sshd crond deamon）是运行的程序，而crontab是用来管理用户的定时任务（规则）的命令

2） crond服务是企业生产工作中常用的重要服务，at和anacron很少用

3） 几乎每个服务器都会用刀crond服务

4） 上千服务器可以开发分布式定时任务项目方案。

#### 5、指令用法 {#175-指令用法}

\[root@oldboy35-moban ~\]\# crontab --help

crontab: invalid option -- '-'

crontab: usage error: unrecognized option

usage: crontab \[-u user\] file

```
crontab \[-u user\] \[ -e \| -l \| -r \]

    \(default operation is replace, per 1003.2\)

-e    \(edit user's crontab\) 编辑修改 当前用户的定时任务   vi /var/spool/cron/root

-l    \(list user's crontab\) 查看/显示 当前用户的定时任务 

-r    \(delete user's crontab\)删除用的定时任务

-i    \(prompt before deleting user's crontab\) 删除之前提示

-s    \(selinux context\)
```

#### 6、指令选项说明

![](https://www.luffycity.com/linux-book/assets/16-4.png)

##### 例子：

\[root@oldboy35-moban ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\#\* \* \* \* \* /usr/sbin/ntpdate ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\#\*/1 \* \* \* \* echo "zzc" &gt;&gt; /server/log/name.log

\[root@oldboy35-moban ~\]\# ls -l /usr/bin/crontab

-rwsr-xr-x. 1 root root 51784 Nov 10 2015 /usr/bin/crontab

#### 7、五个星的解释 {#177-五个星的解释}

通过crontab我们可以用固定的时间间隔执行指定的系统指令或script脚本。时间间隔的单位可以是分、时、日、月、周及以上的任意组合（注意：日和周不要重复，也就是说规定了日就不要在规定周了）。crond服务通过crontab命令可以很容易的实现周期性的日志分析或数据备份等去也运维场景工作。

\[root@oldboy35-moban ~\]\# cat /etc/crontab

SHELL=/bin/bash

PATH=/sbin:/bin:/usr/sbin:/usr/bin

MAILTO=root

HOME=/

\# For details see man 4 crontabs

\# Example of job definition:

\# .---------------- minute \(0 - 59\) 分

\# \| .------------- hour \(0 - 23\) 时

\# \| \| .---------- day of month \(1 - 31\) 日

\# \| \| \| .------- month \(1 - 12\) OR jan,feb,mar,apr ... 月

\# \| \| \| \| .---- day of week \(0 - 6\) \(Sunday=0 or 7\) OR sun,mon,tue,wed,thu,fri,sat 周

\# \| \| \| \| \|

\# \* \* \* \* \* user-name command to be executed

![](https://www.luffycity.com/linux-book/assets/16-1.png)

##### 提示：时间记忆口诀：分时日月周。取值范围记忆：正常日期时间范围，小学生都会的了 {#提示：时间记忆口诀：分时日月周。取值范围记忆：正常日期时间范围，小学生都会的了}

#### 8、时间段的表格 {#178-----时间段的表格}

| **段** | **含义** | **取值范围（整数）** |
| :--- | :--- | :--- |
| **第一段** | 代表分钟 | 00-59（00或者0） |
| **第二段** | 代表小时 | 00-23 |
| **第三段** | 代表日，天 | 01-31 |
| **第四段** | 代表月份 | 01-12 |
| **第五段** | 代表星期，周几 | 0-7（0和7都代表星期日） |

#### 9、crontab 语法格式中特殊符号含义如下表 {#179-crontab-语法格式中特殊符号含义如下表}

| **特殊符号** | **含义** |
| :--- | :--- |
| \* | \*号，表示任意时间都，实际就是“每”的意思 |
| - | 减号表示分隔符，表示一个时间范围，区间段，如17-19点，例如：每天的17，18，19点的00分执行任务。00 17-19 \* \* \* cmd |
| ， | 逗号，表示分隔时段的意思例如每天的5点10点00分执行任务，00 5,10 \* \* \* cmd |
| /n | n代表数字，即“每隔n单位时间”，例如：每10分钟执行一次任务可以写成_/10_\* \* \* cmd，其中，_/10,_的范围是0-59，因此也可以写成0-59/10 |

#### ![](https://www.luffycity.com/linux-book/assets/16-2.png)10、定时任务的步骤

\#\#\#\#第一个里程碑-准备环境

mkdir

\#\#\#\#第二个里程碑-命令行执行命令--是否好使

tar或者

升级版

cd / && tar放包目录.tar.gz要打包的目录

\#\#\#\#第三个里程碑-放入到脚本（文件） xxxx.sh

/bin/sh xxx.sh

\#\#\#\#第四个里程碑-写入到定时任务里面

\* \* \* \* \* /bin/sh xxx.sh /dev/null 2&gt;&1

升级版

写真正的定时任务

\#\#\#\#第五个里程碑-检查并修改定时任务执行时间

tail -f /var/log/cron

ls目录

#### 11、定时任务的实例 {#1710-定时任务的实例}

① 30 3,12 \* \* \* /bin/sh /scripts/oldboy.sh

每天的凌晨3点或12点 半 执行

② 30 \*/6 \* \* \* /bin/sh /scripts/oldboy.sh

每6个小时的半点执行

③ 30 8-18/2 \* \* \* /bin/sh /scripts/oldboy.sh

```
 早上8点到18点每隔2个小时 的半点执行 脚本 

 8,9,10,11,12,13,14,15,16,17,18

 30 8,10,12,14,16,18 \* \* \*  /bin/sh /scripts/oldboy.sh
```

④ 30 21 \* \* \* /application/apache/bin/apachectl graceful

```
 每天的21点30分执行 重启apache软件
```

⑤ 45 4 1,10,22 \* \* /application/apache/bin/apachectl graceful

```
 每个月1,10,22号 凌晨4点45分 重启apache软件
```

⑥ 10 1 \* \* 6,0 /application/apache/bin/apachectl graceful

```
 周六 周日的 凌晨1点10分  重启apache软件
```

⑦ 0,30 18-23 \* \* \* /application/apache/bin/apachectl graceful

```
 18到23点 整点和半点执行  重启apache软件

 0,30 18,19,20,21,22,23 重启apache软件
```

⑧ 00 \*/1 \* \* \* /application/apache/bin/apachectl graceful

```
 00 \* \* \* \* /application/apache/bin/apachectl graceful
```

⑨ \* 23,00-07/1 \* \* \* /application/apache/bin/apachectl graceful

```
 \* 23 \* \* \* \* /application/apache/bin/apachectl graceful

 00 23,00-07/1 \* \* \* /application/apache/bin/apachectl graceful
```

01 \* \* \* \* cmd \#每小时的01分钟执行

字面意思上是什么时间

然后在想多久执行一次

02 04 \* \* \* cmd \#每天4点的02分钟执行

22 14 \* \* 00 cmd \#每周日的14点22分执行

42 04 01 \* \* cmd \#每月1日的4点42分执行

#### 12、小结 {#1711-小结}

1）cmd为要执行的命令或脚本，例如：/bin/sh /server/scripts/chensiqi.sh

2）每个列之间必须要有一个空格。多个空格可以么？自己实践

3）第一个里程碑：把字面的翻译成实际的时间（这里不用考虑多久一次/重复）

4）第二个里程碑：思考多久重复一次或者思考下一次执行是什么时候

##### 强调：周和日不能同时设置使用 {#强调：周和日不能同时设置使用}

#### 12、实例 打印自己的名字

\#\#\#第一个里程碑-准备环境

\[root@oldboy35-moban ~\]\# mkdir -p /server/log

\#\#\#第二个里程碑-命令试试

\[root@oldboy35-moban ~\]\# echo zhaozhichao &gt;&gt;/server/log/name.log

\[root@oldboy35-moban ~\]\# cat /server/log/name.log

zhaozhichao

\#\#\#第三个里程碑-写入到定时任务

\[root@oldboyedu35-nb ~\]\#

\[root@oldboy35-moban ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\* \* \* \* \* /usr/sbin/ntpdate ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\*/1 \* \* \* \* echo "zhaozhichao" &gt;&gt; /server/log/name.log

\#\#\#第四个里程碑-查看-检查

\[root@oldboy35-moban ~\]\# tail -f /server/log/name.log

zhaozhichao

zhaozhichao

#### 13、总结

1）定时任务要加注释

2）如果已经要定向到文件（把命令或脚本的结果放到文件）中，结尾不要有&gt;/dev/null 2&gt;&1

3）/server/log 目录必须要存在才能出结果，如没有创建这个目录

4）定时任务中的路径一定要绝对路径

5）crond服务必须首先开启

6）查看定时任务日志 tail /var/log/cron

