##### 已知如下命令及结果： {#已知如下命令及结果：}

\[oldboy@test ~\]$ echo "I am oldboy,myqq is 31333741"&gt;&gt;oldboy.txt

\[oldboy@test ~\]$ cat oldboy.txt

I am oldboy,myqq is 31333741

##### 现在需要从文件中过滤出“oldboy”和“31333741”字符串，请给出命令 {#现在需要从文件中过滤出oldboy和31333741字符串，请给出命令}

##### 创建环境 {#创建环境}

mkdir /oldboy

echo "I am oldboy,myqq is 31333741"&gt;/oldboy/oldboy.txt

\[root@oldboy36 oldboy\]\# cd /oldboy/

\[root@oldboy36 oldboy\]\# cat oldboy.txt

I am oldboy,myqq is 31333741

##### 方法1 sed+sed {#191-方法1--sedsed}

\[root@oldboy36 oldboy\]\# sed 's\#I am \#\#' oldboy.txt \|sed 's\#,myqq is\#\#'

oldboy 31333741

##### 方法2 cut+sed {#192--方法2--cutsed}

\[root@oldboy36 oldboy\]\# cut -d " " -f3,5 oldboy.txt \|sed 's\#,myqq\#\#'

oldboy 31333741

\[root@oldboy36 oldboy\]\# sed 's\#,\# \#' oldboy.txt \|cut -d ' ' -f3,6

oldboy 31333741

##### 方法3 awk+sed {#193--方法3--awksed}

\[root@oldboy36 oldboy\]\# awk '{print $3,$5}' oldboy.txt \|sed 's\#,myqq\#\#'

oldboy 31333741

\[root@oldboy36 oldboy\]\# sed 's\#,\# \#' oldboy.txt \|awk '{print $3,$6}'

oldboy 31333741

##### 方法4 awk {#194--方法4--awk}

\[root@oldboy36 oldboy\]\# awk -F "\[, \]" '{print $3,$6}' oldboy.txt

oldboy 31333741

\[root@oldboy36 oldboy\]\# awk -F "\[, \]" '{print $3,$NF}' oldboy.txt

oldboy 31333741

\[root@oldboy36 oldboy\]\# awk -F "\[ ,\]" '{print $3","$6}' oldboy.txt

oldboy,31333741

##### 方法5 cut {#195--方法5--cut}

\[root@oldboy36 oldboy\]\# cut -c6-11,20- oldboy.txt

oldboy 31333741

#### wc 统计数量

#### 如何查看/etc/services 文件内容有多少行？

\[root@oldboy36 oldboy\]\# wc -l /etc/services

10774 /etc/services

\[root@oldboy36 oldboy\]\# grep -n . /etc/services \|tail -1

10774:iqobject 48619/udp \# iqobject

#  {#第21章}

#### 过滤出/etc/services 文件包含 3306 或 1521 两数据库端口的行的内容

\[root@oldboy36 oldboy\]\# egrep "3306\|1521" /etc/services

mysql 3306/tcp \# MySQL

mysql 3306/udp \# MySQL

ncube-lm 1521/tcp \# nCube License Manager

ncube-lm 1521/udp \# nCube License Manager

\[root@oldboy36 oldboy\]\# grep "3306\\|1521" /etc/services

mysql 3306/tcp \# MySQL

mysql 3306/udp \# MySQL

ncube-lm 1521/tcp \# nCube License Manager

ncube-lm 1521/udp \# nCube License Manager

