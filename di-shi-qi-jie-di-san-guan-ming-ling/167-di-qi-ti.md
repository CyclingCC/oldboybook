### date命令 {#17--date命令}

\[root@oldboy ~\]\# LANG=en

\[root@oldboy ~\]\# date

Mon Mar 21 08:36:28 CST 2016

\[root@oldboy ~\]\#

\[root@oldboy ~\]\#

\[root@oldboy ~\]\#

\[root@oldboy ~\]\# date -s "2016/05/01"

Sun May 1 00:00:00 CST 2016

\[root@oldboy ~\]\# date

Sun May 1 00:00:02 CST 2016

\[root@oldboy ~\]\# date -s "20160501"

Sun May 1 00:00:00 CST 2016

\[root@oldboy ~\]\# date -s "20160501 11:45:00"

Sun May 1 11:45:00 CST 2016

\[root@oldboy ~\]\# date -s "20160502 11:45:00"

Mon May 2 11:45:00 CST 2016

\[root@oldboy ~\]\# date -s "05/05/2016"

Thu May 5 00:00:00 CST 2016

\[root@oldboy ~\]\# hwclock -w

#### 请给出如下格式的date命令例：11-02-26。在给出实现按周输出比如：周六输出为6，请分别给出命令

\[root@oldboy oldboy\]\# date +%F

2016-04-03

\[root@oldboy oldboy\]\# date +%Y-%m-%d %H:%M:%S

2016-04-03 11:50:24

\[root@oldboy oldboy\]\# date +%F %T

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

