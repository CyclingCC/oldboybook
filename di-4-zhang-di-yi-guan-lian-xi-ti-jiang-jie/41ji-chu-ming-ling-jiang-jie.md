#### 1、linux命令操作语法

命令 \[参数选项\] \[ 文件或路径\]

| 命令 | 空格 | \[参数选项\] | 空格 | \[文件或路径\] |
| :--- | :--- | :--- | :--- | :--- |
| cat | 至少一个空格 | -n | 至少一个空格 | /etc/hosts |

#### 2、创建目录 mkdir

\[root@oldboy ~\]\# mkdir /data

##### 例子：

请用一条命令完成创建目录/oldboy/test，即创建/oldboy目录及/oldboy/test目录

\[root@oldboy ~\]\# mkdir /oldboy/test -p

#### 3、查看目录下的内容 ls

\[root@centos69 ~\]\# ls /data/

\[root@centos69 ~\]\# ls -l /data/

total 0

#### 4、查看目录本身 ls

\[root@centos69 ~\]\# ls -d /data/

/data/

\[root@centos69 ~\]\# ls -ld /data/

drwxr-xr-x 2 root root 4096 May 2 12:10 /data/

#### 5、切换目录 cd

\[root@oldboy ~\]\# cd /

#### 6、相对路径和绝对路径

##### 绝对路径：从/\(根\)开始的路径

cat /etc/sysconfig/network-scripts/ifcfg-eth0

##### 相对路径:不从/\(根\)开始

etc/sysconfig/network-scripts/

##### 例子：

\[root@oldboy /\]\# cd /etc &lt;==绝对路径

\[root@oldboy etc\]\# cd sysconfig/ &lt;==相对路径，相对于谁？相对于命令行里前面etc目录的

\[root@oldboy sysconfig\]\# cd /dev &lt;==绝对路径

\[root@oldboy sysconfig\]\# cd /data

#### 7、查看当前所在路径 pwd

\[root@oldboy data\]\# pwd

/data

#### 8、文件操作

在/data下面建立一个文件oldboy.txt

创建文件

\[root@oldboy data\]\# touch oldboy.txt

\[root@oldboy data\]\# ls

oldboy.txt

\[root@oldboy data\]\# touch /data/oldboy.txt

root@oldboy etc\]\# cd /data

\[root@oldboy data\]\# pwd

/data

\[root@oldboy data\]\# vi oldboy.txt

#### 9、cp命令

##### cp 拷贝文件或目录 默认只能拷贝文件

##### cp命令格式

cp \[OPTION\]... SOURCE... DIRECTORY

cp \[选项\] 文件（或目录）... 目录

cp \[OPTION\]... -t DIRECTORY SOURCE...

cp \[选项\] -t 目录 文件（或目录）...

##### 参数选项

-r \(递归\) 拷贝目录

-p 保持属性

-a 完全拷贝 相当于 -pdr

##### 例子：

##### i、把oldboy.txt文件拷贝到/tmp下

cp /data/oldboy.txt /tmp/

cp -r /data /tmp/

##### ii、已知/tmp下已经存在test.txt文件，如何执行命令才能把/mnt/test.txt拷贝到/tmp下覆盖掉/tmp/test.txt，而让系统不提示是否覆盖，cp不提示：

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

#### 10、mv命令

##### mv命令格式

mv \[OPTION\]... SOURCE... DIRECTORY

mv \[选项\]... 文件（或目录）... 目录

mv \[OPTION\]... -t DIRECTORY SOURCE...

mv \[选项\]... -t 目录 文件（或目录）

##### mv 移动文件或目录（改名）

##### 例子：

把/data目录移动到/root下

\[root@oldboy tmp\]\# mv /data /root/

\[root@oldboy tmp\]\# mkdir stu{11..20}

\[root@oldboy tmp\]\# ls

oldboy.txt stu12 stu14 stu16 stu18 stu20

stu11 stu13 stu15 stu17 stu19

\[root@oldboy tmp\]\# mkdir \`seq 10\`

\[root@oldboy tmp\]\# ls

1 2 4 6 8 oldboy.txt stu12 stu14 stu16 stu18 stu20

10 3 5 7 9 stu11 stu13 stu15 stu17 stu19

##### 操作习惯

目录下的内容，不包括目录data本身

mv /data/\* /tmp/

目录及下面的内容，包含目录 data本身

mv /data /tmp/

实际上 cp mv 源/data和/data/一致，目标/tmp如果不存在就把/data改为/tmp

rsync特殊

#### 11、rm命令

##### rm 删除文件或目录 默认只能删文件 -f强制 -r删除目录（递归）

##### 习惯: 慎用rm 使用mv或者find代替 空间不允许时，先备份，再删除

##### 进入/root目录下的data目录，删除oldboy.txt文件

##### 退出到上一级目录，删除data目录

##### 例子：

cd /root/data

rm oldboy.txt -f

cd ..

rm /data -r

##### 修改系统时间

date -s "2016-03-22"

##### 面试题：删除一个目录下的所有文件，但保留一个指定文件

[http://oldboy.blog.51cto.com/2561410/1650380](http://oldboy.blog.51cto.com/2561410/1650380)

解答：

假设这个目录是/xx/，里面有file1,file2,file3..file10 十个文件

\[root@oldboy xx\]\# touch file{1..10}

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

方法一：find

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# find /xx -type f ! -name "file10"\|xargs rm -f

\[root@oldboy xx\]\# ls

file10

\[root@oldboy xx\]\# find /xx -type f ! -name "file10" -exec rm -f {} \;

\[root@oldboy xx\]\# ls

file10

方法二：rsync

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# rsync -az --delete --exclude "file10" /null/ /xx/

\[root@oldboy xx\]\# ls

file10

方法三:开启bash的extglob功能\(此功能的作用就是用rm !\(\*jpg\)这样的方式来删除不包括号内文件的文件\)

\[root@oldboy xx\]\# shopt -s extglob

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# rm -f !\(file10\)

\[root@oldboy xx\]\# ls

file10

方法四：

find ./ -type f\|grep -v "\boldboy1\b"\|xargs rm -f

方法五：

rm -f \`ls\|grep -v "\boldboy1\b"\`

##### 从运维角度，任何删除性的操作都应该事先备份后在执行或者确认有备份存在。

#### 12、find命令

##### find命令格式

find 在哪找\(目录\) 找什么类型\(-type\) 叫什么\(-name\) ... ... ...

find /data -type \[ f d ...\] -name "\*.txt"

##### find 查找文件或目录

\[root@oldboy ~\]\# find / -type f -name "oldgirl.txt"

/data1/oldgirl.txt

find / -type f -name "oldgirl.txt" -exec rm {} \;

find /data -type f -name "oldboy.txt" -mtime +7 -exec rm {} \;

##### 参数

-type f d

-name

-mtime \(+7 7 -7\)

-exec 行动

##### mtime +7 修改时间7天前

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

cp \`find /data -type f -name "oldboy.txt"\` /tmp/

##### 企业面试题：查找/oldboy下所有7天前的以log结尾的文件移动到/tmp下

find /oldboy/ -type f -name "\*.log" -mtime +7 -exec mv {} /tmp/ \;

[http://oldboy.blog.51cto.com/2561410/1750481](http://oldboy.blog.51cto.com/2561410/1750481)

##### i、管道：前面的输出结果给后面的命令管道后面不支持命令别名

##### 命令的输出结果经过管道后变成了字符串（数据流），是一个整体 {#命令的输出结果经过管道后变成了字符串（数据流），是一个整体}

\[root@oldboy data\]\# touch {1..10}.txt

\[root@oldboy data\]\# find /data -type f -name "\*.txt"

/data/10.txt

/data/4.txt

/data/8.txt

/data/2.txt

/data/5.txt

/data/6.txt

/data/1.txt

/data/3.txt

/data/9.txt

/data/7.txt

\[root@oldboy data\]\# find /data -type f -name "\*.txt" \|xargs ls -l

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/10.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/1.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/2.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/3.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/4.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/5.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/6.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/7.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/8.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/9.txt

find /data -type f -name "\*.txt" \|xargs -i mv {} /tmp/

#### 3种方法： {#3种方法：}

cp \`find /data -type f -name "oldboy.txt" -mtime +7\` /tmp/

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

find /data -type f -name "oldboy.txt"\|xargs -i cp {} /tmp/

##### ii、xargs 又称管道命令，构造参数等。是给命令传递参数的一个过滤器,也是组合多个命令的一个工具 它把一个数据流分割为一些足够小的块,以方便过滤器和命令进行处理 。简单的说 就是把 其他命令的给它的数据 传递给它后面的命令作为参数

##### xargs 从标准输入获取内容创建和执行命令

-n 数字 做分组，几个一组 -i {}

\[root@oldboy ~\]\# echo 1 2 3 4 &gt;a.txt

\[root@oldboy ~\]\# cat a.txt

1 2 3 4

\[root@oldboy ~\]\# xargs -n 2 &lt; a.txt

1 2

3 4

\[root@oldboy ~\]\# find /data/ -type d -name "\*.txt"

/data/10.txt

/data/4.txt

/data/8.txt

/data/2.txt

/data/5.txt

/data/6.txt

/data/1.txt

/data/3.txt

/data/9.txt

/data/7.txt

\[root@oldboy ~\]\# find /data/ -type d -name "\*.txt" \|xargs -n 2

/data/10.txt /data/4.txt

/data/8.txt /data/2.txt

/data/5.txt /data/6.txt

/data/1.txt /data/3.txt

/data/9.txt /data/7.txt

#### 13、head命令

##### 显示文件前面的内容 默认前10行

\[root@oldboy data\]\# head -2 test.txt

test

liyao

#### 14、tail命令

##### 显示文件的尾部内容，默认后10行

\[root@oldboy data\]\# tail -2 test.txt

liyao

oldboy

#### 15、seq命令

##### Linux 中一个预设的外部命令，一般用作一堆数字的简化写法

\[root@oldboy data\]\# seq 1 2 9 \|xargs

1 3 5 7 9

\[root@oldboy data\]\# seq -s " " 5

1 2 3 4 5

\[root@oldboy data\]\# seq -s "-" 5

1-2-3-4-5

#### 16、tree命令

##### 显示目录结构

tree /root/

/root/

├── anaconda-ks.cfg

├── init.sh

├── install.log

├── install.log.syslog

└── sersync.tar.gz

0 directories, 5 files

#### 17、cat命令

\[root@oldboy data\]\# cat &gt;a.txt

oldboy

\[root@oldboy data\]\# cat a.txt

oldboy

\[root@oldboy data\]\# cat &gt;&gt;/data/oldboy.txt &lt;&lt;EOF

&gt; I am studying linux.

&gt; EOF

#### 练习题：

1、说出已学习过的10个命令及如何使用？

2、查找/oldboy下所有7天前的以log结尾的文件移动到/tmp下

3、删除一个目录下的所有文件，但保留一个指定文件

