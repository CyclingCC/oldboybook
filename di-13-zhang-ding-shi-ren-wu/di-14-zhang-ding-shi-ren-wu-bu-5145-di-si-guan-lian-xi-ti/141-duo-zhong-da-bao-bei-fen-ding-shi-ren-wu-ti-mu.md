#### 1、 每隔 1 分钟，打印一个+号到 oldboy.log ,请给出 crontab 完整命令。

解答：

\*/1 \* \* \* \*  echo + &gt;&gt;/server/log/oldboy.log

写一个定时任务：

\#\#\#1.创建环境

mkdir -p /server/log/

\#\#\#2.命令行测试

echo + &gt;&gt; /server/log/jiahao.log

\#\#\#3.写入到定时任务

\#\#xianshi   +  lidao xxxxx

\* \* \* \* \* /bin/echo   + &gt;&gt; /server/log/jiahao.log

\#\#\#4.检查结果

tail -f /server/log/jiahao.log

\#\#\#5.定时任务日志

tail /var/log/cron

\* \* \* \* \* /bin/echo   + &gt;&gt; /server/log/jiahao.log

#### 2、 每隔 2 个小时将/etc/services 文件打包备份到/tmp 下（最好每次备份成不同的备份包）。

解答：

\* \*/2 \* \* \*

\#\#\#第一个里程碑-打包

\[root@oldboyedu35-nb test\]\# tar zcf /tmp/serivces.tar.gz /etc/services

tar: Removing leading \`/' from member names

\[root@oldboyedu35-nb test\]\# tar tf /tmp/serivces.tar.gz

etc/services

\#\#\#\#第二个里程碑-打包-每个包不同-加上时间

\#tar zcf /tmp/services.时间.tar.gz  /etc/services

tar zcf /tmp/services.$\(date +%F-%H\).tar.gz  /etc/services

tar: Removing leading \`/' from member names

ll /tmp/ser\*

\#\#\#\#第三个里程碑-脚本里面及测试脚本

cat /server/scripts/tar.sh

/bin/tar zcf /tmp/services.$\(date +%F-%H\).tar.gz  /etc/services

/bin/sh  /server/scripts/tar.sh

/bin/tar: Removing leading \`/' from member names

ll /tmp/ser\*

-rw-r--r-- 1 root root 127303 Apr  1 11:59 /tmp/serivces.tar.gz

-rw-r--r-- 1 root root 127303 Apr  1 12:05 /tmp/services.2017-04-01-12.tar.gz

\#\#\#\#第四个里程碑-写入到定时任务里面

\#print dabao

\* \* \* \* \* /bin/sh /server/scripts/dabao.sh &gt;&gt; /server/log/dabao.log 2&gt;&1

\#\#\#\#第五个里程碑-写入到定时任务里面

\#print dabao

00 \*/2 \* \* \* /bin/sh /server/scripts/dabao.sh &gt;&gt; /server/log/dabao.log 2&gt;&1

脚本升级：

cd /etc/ && tar zcf /tmp/services.$\(date +%F-%H\).tar.gz  services

把命令或脚本执行中显示到屏幕上的东西 （命令执行中的废料） 定向到空或文件

#### 3、每天晚上 12 点，打包站点目录/var/www/html 备份到/data 目录下（最好每次备份按时间

生成不同的备份包）

解答：

00 00 \* \* \*

\#\#\#\#第一个里程碑-准备环境

mkdir -p /var/www/html /data

\#\#\#\#第二个里程碑-命令行执行命令--是否好使

\#tar zcf /tmp/services.时间.tar.gz  /etc/services

\#tar zcf /tmp/services.$\(date +%F-%H\).tar.gz  /etc/services

cd / && tar zcf /tmp/services.$\(date +%F-%H\).tar.gz  etc/services

\#\#\#\#第三个里程碑-放入到脚本（文件）  xxxx.sh

\[root@oldboy35-moban ~\]\# cat /server/scripts/html.sh

cd / && tar zcf /data/html\_$\(date +F-%M-%H-%S\).tar.gz var/www/

\#\#\#\#第四个里程碑-写入到定时任务里面

\#print dabao html

00 00 \* \* \* /bin/sh /server/scripts/html.sh &gt;/dev/null 2&gt;&1

\#\#\#\#第五个里程碑-检查并修改定时任务执行时间

\#print dabao html

\* \* \* \* \* /bin/sh /server/scripts/html.sh &gt;/dev/null 2&gt;&1

\#\#\#\#第六个里程碑-查看是否成功两个地方

日志 tail -f /var/log/cron

打包文件 ll /data

#### 4、每周 六、日 上午 9:00 和下午 14： 00 来老男孩这里学习\(执行程序/server/script/oldboy.sh

代替学习\)。

解答：

00 9,14 \* \* 6,0 /bin/sh /server/script/oldboy.sh /dev/null 2&gt;&1

#### 5、请描述下列路径的内容是做什么的？

/etc/sysctl.conf  系统内核的配置文件

/etc/rc.local    开机自启动的命令

/etc/hosts      ip与域名的解析关系

/etc/fstab      开机自启动挂载的列表

/var/log/secure 用户登录信息

解答：

#### 6、请说出下列 grep 正则表达式的含义

^  以什么开头

$  以什么结尾

.\(点号\) 任意一个字符

\*  重复前一个字符（文本）0次或多次

{n,m} 表示n或m重复 连续

\[^t\] \#\#\#找到不是t这个字母的文字 文本  内容

^\[^t\] \#\#\#\#\#以不是字母t开头的行

\[t\]  \#\#\#找到t这个字母

解答：

#### 7、授权 oldboy 目录及其子目录 755 的权限，请给出命令。

解答：

chmod -R 755 /oldboy/

#### 8、把 oldboy 目录及其子目录的属主改为 oldboy,组改为 root,请给出命令。

解答：

chown -R oldboy:root /oldboy/

#### 9、描述下 umask 的作用，并举例。

解答：

umask：权限掩码。作用：配置文件的默认权限。

root用户umask值默认为：0022

新建一个文件时，文件的权限肯定是644（666-022）

新建一个目录时，目录的权限肯定是755（777-022）

原因：目录权限755和文件权限644是一个目录或普通文件安全的边界。

#### 10、添加一个用户 oldboy，并指定属于 sa 组，要求组 ID 为 801， uid 为 808,并且不建立家目录及禁止其登陆。

解答：

\[root@oldboy35-moban ~\]\# groupadd -g 801 sa

\[root@oldboy35-moban ~\]\# useradd -u 808 -g sa -M -s /sbin/nologin IanA

#### 11、如何查看用户的 uid 及属于的组信息。

解答：

\[root@oldboy35-moban ~\]\# id

uid=0\(root\) gid=0\(root\) groups=0\(root\) context=unconfined\_u:unconfined\_r:unconfined\_t:s0-s0:c0.c1023

#### 练习题：

1、每周1的凌晨 2 点半小时将/etc/services 文件打包备份到/tmp 下（最好每次备份成不同的备份包）。

2、添加一个用户 oldboy，并指定属于 sa 组，要求组 ID 为 999， uid 为 808,并且不建立家目录及禁止其登陆。

