两种情况

#### linux系统自身定期执行的任务工作： {#151-linux系统自身定期执行的任务工作：}

系统周期性自行执行的任务工作，如轮循系统日志、备份系统数据、清理系统缓存等，这些任务无需我们认为干预。

\[root@oldboy35-moban ~\]\# ls -l /var/log/messages\*

-rw-------. 1 root root 183394 Mar 31 17:16 /var/log/messages

-rw-------. 1 root root 562454 Mar 21 09:03 /var/log/messages-20170321

-rw-------. 1 root root 131826 Mar 27 09:38 /var/log/messages-20170327

\[root@oldboy35-moban ~\]\# ls -l /var/log/secure\*

-rw-------. 1 root root 7833 Mar 31 11:58 /var/log/secure

-rw-------. 1 root root 6162 Mar 21 09:03 /var/log/secure-20170321

-rw-------. 1 root root 1644 Mar 27 08:35 /var/log/secure-20170327

#### 用户执行的任务工作：某个用户或系统管理员定期要做的任务工作 {#152-用户执行的任务工作：某个用户或系统管理员定期要做的任务工作}

例如：服务器时间的同步

\[root@oldboyedu35-nb ~\]\# cat /var/spool/cron/root

cat: /var/spool/cron/root: No such file or directory

\[root@oldboyedu35-nb ~\]\# crontab -l

no crontab for root

##### 命令行执行命令--是否好使 {#1521-命令行执行命令--是否好使}

\[root@oldboyedu35-nb ~\]\# ntpdate ntp1.aliyun.com

31 Mar 11:02:59 ntpdate\[13433\]: adjust time server 182.92.12.11 offset 0.000046 sec

##### 命令要写绝对路径 {#1522-命令要写绝对路径}

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# which ntpdate

/usr/sbin/ntpdate

\[root@oldboyedu35-nb ~\]\# /usr/sbin/ntpdate ntp1.aliyun.com

31 Mar 11:03:51 ntpdate\[13440\]: adjust time server 182.92.12.11 offset -0.001770 sec

##### 命令行测试ok--写入到定时任务中 {#1523命令行测试ok--写入到定时任务中}

\[root@oldboyedu35-nb ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\* \* \* \* \* /usr/sbin/ntpdate ntp1.aliyun.com &gt;/dev/null 2&gt;&1

\[root@oldboyedu35-nb ~\]\# date -s "1000 day"

Thu Dec 26 11:06:26 CST 2019

\[root@oldboyedu35-nb ~\]\# date

Thu Dec 26 11:07:04 CST 2019

\[root@oldboyedu35-nb ~\]\# date

Fri Mar 31 11:07:06 CST 2017

##### 修改 每个10分钟 {#1524-修改-每个10分钟}

crontab: installing new crontab

\[root@oldboyedu35-nb ~\]\# crontab -l

\#sync time lidao 2017xxxxx

\*/10 \* \* \* \* /usr/sbin/ntpdate ntp1.aliyun.com &gt;/dev/null 2&gt;&1

