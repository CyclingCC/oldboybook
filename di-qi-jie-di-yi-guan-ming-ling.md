# 第1章 linux命令

## 1.1  linux命令操作语法

命令   \[参数选项\]   \[ 文件或路径\]

| 命令 | 空格 | \[参数选项\] | 空格 | \[文件或路径\] |
| :--- | :--- | :--- | :--- | :--- |
| cat | 至少一个空格 | -n | 至少一个空格 | /etc/hosts |

## 1.2  目录操作

目录用于存放目录或文件

创建一个目录 /data

### 1.2.1  创建目录  mkdir

\[root@oldboy ~\]\# mkdir /data

请用一条命令完成创建目录/oldboy/test，即创建/oldboy目录及/oldboy/test目录

mkdir /oldboy/test -p

### 1.2.2  查看目录下的内容  ls

\[root@centos69 ~\]\# ls /data/

\[root@centos69 ~\]\# ls -l /data/

total 0

### 1.2.3  查看目录本身  ls

\[root@centos69 ~\]\# ls -d /data/

/data/

\[root@centos69 ~\]\# ls -ld /data/

drwxr-xr-x 2 root root 4096 May  2 12:10 /data/

### 1.2.4  切换目录  cd

\[root@oldboy ~\]\# cd /

### 1.2.5  相对路径和绝对路径

##### 绝对路径：从/\(根\)开始的路径

cat /etc/sysconfig/network-scripts/ifcfg-eth0

##### 相对路径:不从/\(根\)开始

etc/sysconfig/network-scripts/

##### 例子：

\[root@oldboy /\]\# cd /etc &lt;==绝对路径

\[root@oldboy etc\]\# cd sysconfig/ &lt;==相对路径，相对于谁？相对于命令行里前面etc目录的

\[root@oldboy sysconfig\]\# cd /dev &lt;==绝对路径

\[root@oldboy sysconfig\]\# cd /data

### 1.2.6  查看当前所在路径  pwd

\[root@oldboy data\]\# pwd

/data

## 1.3  文件操作

在/data下面建立一个文件oldboy.txt

### 1.3.1 创建文件

\[root@oldboy data\]\# touch oldboy.txt

\[root@oldboy data\]\# ls

oldboy.txt

\[root@oldboy data\]\# touch /data/oldboy.txt

root@oldboy etc\]\# cd /data

\[root@oldboy data\]\# pwd

/data

\[root@oldboy data\]\# vi oldboy.txt

# 第2章 vi/vim 文本编辑器

![](/assets/7-1.png)

#### 字符集

LANG=zh\_CN.UTF-8

#### 辅助工具

vim手册

vimtutor

# 第3章 输入输出重定向

1. &gt; 或 1&gt;    输出重定向，会清楚文件里所有的数据，增加新的内容
2. &gt;&gt; 或 1&gt;&gt;  追加输出重定向，文件的结尾加入内容，不会删除已有的文件数据
3. &lt;   输入重定向
4. &lt;&lt;  追加输入重定向
5. 2&gt;    错误重定向
6. 2&gt;&gt;   错误追加重定向

1、标准输入（stdin）：代码0，使用 &lt; 或 &lt;&lt; 数据流向从右向左

2、标准输出（stdout）: 代码1，使用 &gt; 或 &gt;&gt;  数据流向从左向右

3、标准错误输出（stderr）: 代码2，使用 2&gt; 或 2&gt;&gt; 数据流向从左向右

## 例子：为oldboy.txt增加内容为“I am studying linux.”

### 3.1 输出重定向

\[root@oldboy data\]\# echo 'I am study linux.' &gt;oldboy.txt

\[root@oldboy data\]\# cat oldboy.txt

I am study linux.

echo 'I am study linux.' &gt;oldboy.txt

1、如果没有oldboy.txt，会创建。

2、如果有oldboy.txt，会清空内容，放入单引号的内容。

\[root@oldboy data\]\# echo -e 'I am study linux\nI am study'&gt;&gt;b.txt

\[root@oldboy data\]\# cat b.txt

I am study linux

I am study

\[root@oldboy data\]\# cho "hello oldboy" &gt; all.txt 2&gt;&1

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

\[root@oldboy data\]\# &gt;all.txt

\[root@oldboy data\]\# cat all.txt

\[root@oldboy data\]\# cho "hello oldboy" &&gt; all.txt

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

\[root@oldboy data\]\# &gt; all.txt

\[root@oldboy data\]\# cat all.txt

\[root@oldboy data\]\# cho "hello oldboy" &gt; all.txt 2&gt; all.txt

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

### 3.2  输入重定向

echo "1 2 3 4 5" &gt;&gt; /data/oldboy.txt

cat /data/oldboy.txt

1 2 3 4 5

xargs -n2 &lt; /data/oldboy.txt

1 2

3 4

5

\[root@oldboy data\]\# cat b.txt

I am study linux

I am study

\[root@oldboy data\]\# xargs -n1 &lt;b.txt

I

am

study

linux

I

am

study

\[root@oldboy data\]\# xargs -n2 &lt;b.txt

I am

study linux

I am

study

echo oldboy 2&gt;a.txt 1&gt;b.txt

echo oldboy &gt;a.txt 2&gt;&1       错误和正确放在一起

### 3.3  cat命令

\[root@oldboy data\]\# cat &gt;a.txt

oldboy

\[root@oldboy data\]\# cat a.txt

oldboy

\[root@oldboy data\]\# cat &gt;&gt;/data/oldboy.txt &lt;&lt;EOF

&gt; I am studying linux.

&gt; EOF

# 第4章 cp命令

## 4.1  cp  拷贝文件或目录    默认只能拷贝文件

## 4.2  cp命令格式

cp   \[OPTION\]...  SOURCE...            DIRECTORY

cp   \[选项\]       文件（或目录）...       目录

cp   \[OPTION\]...   -t  DIRECTORY       SOURCE...

cp   \[选项\]        -t  目录              文件（或目录）...

## 4.3 参数选项

-r   \(递归\)  拷贝目录

-p  保持属性

-a  完全拷贝  相当于 -pdr

## 把oldboy.txt文件拷贝到/tmp下

cp /data/oldboy.txt /tmp/

cp -r /data /tmp/

## 已知/tmp下已经存在test.txt文件，如何执行命令才能把/mnt/test.txt拷贝到/tmp下覆盖掉/tmp/test.txt，而让系统不提示是否覆盖

## cp不提示：

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

# 第5章 mv命令

## 5.1  mv命令格式

mv    \[OPTION\]...    SOURCE...         DIRECTORY

mv    \[选项\]...       文件（或目录）...   目录

mv    \[OPTION\]...    -t DIRECTORY     SOURCE...

mv    \[选项\]...       -t 目录            文件（或目录）

## 5.2 mv   移动文件或目录（改名）

把/data目录移动到/root下

\[root@oldboy tmp\]\# mv /data /root/

\[root@oldboy tmp\]\# mkdir stu{11..20}

\[root@oldboy tmp\]\# ls

oldboy.txt  stu12  stu14  stu16  stu18  stu20

stu11       stu13  stu15  stu17  stu19

\[root@oldboy tmp\]\# mkdir \`seq 10\`

\[root@oldboy tmp\]\# ls

1   2  4  6  8  oldboy.txt  stu12  stu14  stu16  stu18  stu20

10  3  5  7  9  stu11       stu13  stu15  stu17  stu19

### 5.3 操作习惯

目录下的内容，不包括目录data本身

mv /data/\* /tmp/

目录及下面的内容，包含目录 data本身

mv /data /tmp/

实际上 cp mv 源/data和/data/一致，目标/tmp如果不存在就把/data改为/tmp

rsync特殊

# 第6章 rm命令

#### 6.1 rm   删除文件或目录   默认只能删文件  -f强制  -r删除目录（递归）

#### 6.2 习惯: 慎用rm  使用mv或者find代替   空间不允许时，先备份，再删除

#### 进入/root目录下的data目录，删除oldboy.txt文件

#### 退出到上一级目录，删除data目录

cd /root/data

rm oldboy.txt -f

cd ..

rm /data -r

#### 6.3 修改系统时间

date -s "2016-03-22"

#### 6.4 面试题：删除一个目录下的所有文件，但保留一个指定文件

[http://oldboy.blog.51cto.com/2561410/1650380](http://oldboy.blog.51cto.com/2561410/1650380)

解答：

假设这个目录是/xx/，里面有file1,file2,file3..file10  十个文件

\[root@oldboy xx\]\# touch file{1..10}

\[root@oldboy xx\]\# ls

file1  file10  file2  file3  file4  file5  file6  file7  file8  file9

方法一：find

\[root@oldboy xx\]\# ls

file1  file10  file2  file3  file4  file5  file6  file7  file8  file9

\[root@oldboy xx\]\# find /xx -type f ! -name "file10"\|xargs rm -f

\[root@oldboy xx\]\# ls

file10

\[root@oldboy xx\]\# find /xx -type f ! -name "file10" -exec rm -f {} \;

\[root@oldboy xx\]\# ls

file10

方法二：rsync

\[root@oldboy xx\]\# ls

file1  file10  file2  file3  file4  file5  file6  file7  file8  file9

\[root@oldboy xx\]\# rsync -az --delete --exclude "file10" /null/ /xx/

\[root@oldboy xx\]\# ls

file10

方法三:开启bash的extglob功能\(此功能的作用就是用rm !\(\*jpg\)这样的方式来删除不包括号内文件的文件\)

\[root@oldboy xx\]\# shopt -s extglob

\[root@oldboy xx\]\# ls

file1  file10  file2  file3  file4  file5  file6  file7  file8  file9

\[root@oldboy xx\]\# rm -f !\(file10\)

\[root@oldboy xx\]\# ls

file10

方法四：

find ./ -type f\|grep -v "\boldboy1\b"\|xargs rm -f

方法五：

rm -f \`ls\|grep -v "\boldboy1\b"\`

#### 从运维角度，任何删除性的操作都应该事先备份后在执行或者确认有备份存在。

# 第7章 find命令

## 7.1 find命令格式

find    在哪找\(目录\)    找什么类型\(-type\)   叫什么\(-name\)     ...     ...     ...

find    /data                     -type  \[ f  d ...\]      -name  "\*.txt"

## 7.2 find    查找文件或目录

\[root@oldboy ~\]\# find / -type f  -name "oldgirl.txt"

/data1/oldgirl.txt

find / -type f  -name "oldgirl.txt" -exec rm {} \;

find /data -type f -name "oldboy.txt" -mtime +7 -exec rm {} \;

## 7.3 参数

-type f d

-name

-mtime \(+7 7 -7\)

-exec 行动

## 7.3 mtime +7  修改时间7天前

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

cp  \`find /data -type f -name "oldboy.txt"\` /tmp/

### 企业面试题：查找/oldboy下所有7天前的以log结尾的文件移动到/tmp下

find /oldboy/ -type f -name "\*.log" -mtime +7 -exec mv {} /tmp/ \;

[http://oldboy.blog.51cto.com/2561410/1750481](http://oldboy.blog.51cto.com/2561410/1750481)

# 第8章 管道 \|

##### 管道：前面的输出结果给后面的命令管道后面不支持命令别名

##### 命令的输出结果经过管道后变成了字符串（数据流），是一个整体

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

#### 3种方法：

cp \`find /data -type f -name "oldboy.txt" -mtime +7\` /tmp/

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

find /data -type f -name "oldboy.txt"\|xargs -i cp {} /tmp/

# 第9章 xargs命令

##### xargs 又称管道命令，构造参数等。是给命令传递参数的一个过滤器,也是组合多个命令的一个工具 它把一个数据流分割为一些足够小的块,以方便过滤器和命令进行处理 。简单的说 就是把 其他命令的给它的数据 传递给它后面的命令作为参数

### 9.1  xargs  从标准输入获取内容创建和执行命令

-n 数字   做分组，几个一组  -i  {}

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

# 第10章 grep命令

#### 10.1  已知文件test.txt内容为：

#### test

#### liyao

#### oldboy

#### 请给出输出test.txt文件内容时，不包含oldboy字符串的命令

#### 10.2 grep  筛子  想要的不想要的分开   默认筛子中的要

\[root@oldboy data\]\# cat test.txt

test

liyao

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt -v

test

liyao

#### 10.3 只查看ett.txt文件（共100行）内第20到第30行的内容

\[root@oldboy ~\]\# grep 20 -A 10 a.txt      记忆方法  after

20

21

22

23

24

25

26

27

28

29

30

\[root@oldboy ~\]\# grep 30 -B 10 a.txt     记忆方法  before

20

21

22

23

24

25

26

27

28

29

30

\[root@oldboy ~\]\# grep 25 -C5 a.txt

20

21

22

23

24

25

26

27

28

29

30

# 第11章 head命令

#### 显示文件前面的内容    默认前10行

\[root@oldboy data\]\# head -2 test.txt

test

liyao

# 第12章 tail命令

#### 显示文件的尾部内容，默认后10行

\[root@oldboy data\]\# tail -2 test.txt

liyao

oldboy

# 第13章 seq

Linux 中一个预设的外部命令，一般用作一堆数字的简化写法

\[root@oldboy data\]\# seq 1  2  9 \|xargs

1 3 5 7 9

\[root@oldboy data\]\# seq -s  " " 5

1 2 3 4 5

\[root@oldboy data\]\# seq -s  "-" 5

1-2-3-4-5

# 第14章 tree命令

#### 显示目录结构

tree /root/

/root/

├── anaconda-ks.cfg

├── init.sh

├── install.log

├── install.log.syslog

└── sersync.tar.gz

0 directories, 5 files

# 第15章 alias命令

#### 15.1 alias 查看别名

\[root@oldboy oldboy\]\# alias

alias cp='cp -i'

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

#### 15.2  设置别名

\[root@oldboy oldboy\]\# alias rm='echo "this command does not allow to use."'

\[root@oldboy oldboy\]\# rm

this command does not allow to use.

echo "alias rm='echo do not use rm' " &gt;&gt; /etc/profile

#### 15.3 取消别名

unalias rm

#### 15.4  别名作用

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp -i a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? ^C

\[root@oldboy oldboy\]\# alias

alias cp='cp -i'

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias rm='rm -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

\[root@oldboy oldboy\]\# unalias cp

\[root@oldboy oldboy\]\# alias

alias l.='ls -d .\* --color=auto'

alias ll='ls -l --color=auto'

alias ls='ls --color=auto'

alias mv='mv -i'

alias rm='rm -i'

alias which='alias \| /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

\[root@oldboy oldboy\]\# alias\|grep cp

\[root@oldboy oldboy\]\# cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp a.txt /tmp/

\[root@oldboy oldboy\]\# cp -i a.txt /tmp/

cp: overwrite \`/tmp/a.txt'?

#### 15.5  定义别名永久生效

source /etc/profile 全局生效

~/.bashrc    当前用户生效

# 第16章 sed命令

sed \*\*\*\*\* 擅长取行，替换，linux三剑客老二

sed  \[选项\]  \[sed命令\]  \[输入文件\]

-n 取消默认输出，功能p\(print\)打印

例：取行：sed -n '20,30p' ett.txt

g与s联合使用时，表示对当前行全局匹配替换，s常说的查找并替换，用一个字符串替换成另一个

-e允许多项编辑

-i修改文件内容（修改磁盘上的内容）

#### 16.1  sed过滤

sed -n '/oldboy/p' test.txt

\[root@oldboy ~\]\# sed -n '20,30p' a.txt

20

21

22

23

24

25

26

27

28

29

30

#### 16.2  sed替换

\[root@oldboy ~\]\# sed 's\#oldgirl\#gongli\#' a.txt

oldboy gongli

gongli

\#是分隔符，分隔符可以是任意的

#### 16.3  sed删除

\[root@oldboy data\]\# cat test.txt

test

liyao

oldboy

\[root@oldboy36 ~\]\# sed -n '/oldboy/!p' oldboy.txt

test

liyao

\[root@oldboy36 ~\]\# sed '/oldboy/d' oldboy.txt

test

liyao

#### 16.4  sed修改文件内容

\[root@oldboy ~\]\# sed -i 's\#oldgirl\#gongli\#g' a.txt

\[root@oldboy ~\]\# cat a.txt

oldboy gongli

gongli

# 第17章 awk命令

#### 17.1 awk   linux三剑客老大

NR  行号

==   等于

$0  整行

\[root@oldboy ~\]\# awk 'NR&gt;19&&NR&lt;31' a.txt

20

21

22

23

24

25

26

27

28

29

30

seq 50 \|awk 'NR==20,NR==30 {print}'

\[root@oldboy36 ~\]\# awk '!/oldboy/' oldboy.txt

test

liyao

\[root@oldboy data\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2 {print $4}'

10.0.0.30

\[root@oldboy oldboy\]\# ifconfig eth0\|sed -nr 's\#^.\*dr:\(.\*\) B.\*$\#\1\#gp'

192.168.33.128

\[root@oldboy oldboy\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2 {print $4}'

192.168.33.128

# 第18章  实战题目

/oldboy目录下文件中内容oldboy替换为oldgirl

#### 18.1  创建环境

mkdir -p /oldboy/test

cd /oldboy

echo "oldboy"&gt;test/del.sh

echo "oldboy"&gt;test.sh

echo "oldboy"&gt;t.sh

touch oldboy.txt

touch alex.txt

#### 18.2  找出文件

\[root@oldboyedu36 oldboy\]\# \#找到你要处理的东西

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f

/oldboy/alex.txt

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/oldboy.txt

/oldboy/t.sh

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

#### 18.3 把一个文件中的oldboy替换为oldgirl

sed 's\#找谁\#替换成啥\#g'

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

oldgirl

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldboy

\[root@oldboyedu36 oldboy\]\# sed -i 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldgirl

#### 18.4 用find命令找到文件，然后用sed修改文件内容

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

\[root@oldboyedu36 oldboy\]\# \#\#先看看结果对不对

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh^C

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh^C

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"\|xargs sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

oldgirl

oldgirl

oldgirl

oldgirl

\[root@oldboyedu36 oldboy\]\# \#\#结果对了 -i

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"\|xargs sed -i 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldgirl

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test/del.sh

oldgirl

#### 18.5  其它方法

方法二

\[root@oldboyedu36 ~\]\# \#\#\#

\[root@oldboyedu36 ~\]\# which mkdir

/bin/mkdir

\[root@oldboyedu36 ~\]\# ls -l /bin/mkdir

-rwxr-xr-x. 1 root root 50056 Mar 23 02:52 /bin/mkdir

\[root@oldboyedu36 ~\]\#

\[root@oldboyedu36 ~\]\# \#\#\#把上面两条命令合起来

\[root@oldboyedu36 ~\]\# \#\#\#ls -l 此处放置的是which mkdir命令的结果

\[root@oldboyedu36 ~\]\# ls -l which mkdir

ls: cannot access which: No such file or directory

ls: cannot access mkdir: No such file or directory

\[root@oldboyedu36 ~\]\# ls -l $\(which mkdir\)

-rwxr-xr-x. 1 root root 50056 Mar 23 02:52 /bin/mkdir

\[root@oldboyedu36 ~\]\# \#\#$\(\)  表示 先执行里面的"命令",然后把命令结果留下来

\[root@oldboyedu36 ~\]\# \#\#$\(\)  =====  \`\`

$\(\)  &lt;==&gt;  \`\`    在一个命令中包含另一个命令

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g'  文件名字 文件 文件 文件

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g'   这些文件怎么得到的？

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g'   find命令的结果

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g'   $\(find /oldboy/ -type f -name "\*.sh"\)

\[root@oldboyedu36 ~\]\# sed 's\#oldboy\#oldgirl\#g'   $\(find /oldboy/ -type f -name "\*.sh"\)

oldgirl

oldgirl

oldgirl

方法三

\[root@oldboyedu36 ~\]\# \#\#\#

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh" -exec ls -l {} \;

-rw-r--r--. 1 root root 7 May  3 06:27 /oldboy/test.sh

-rw-r--r--. 1 root root 7 May  3 06:27 /oldboy/test/del.sh

-rw-r--r--. 1 root root 7 May  3 06:27 /oldboy/t.sh

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh" -exec sed 's\#oldboy\#oldgirl\#g' {} \;

oldgirl

oldgirl

oldgirl

#### 18.6  修改网卡ip

find /etc/ -type f -name "\*eth0" \|xargs sed 's\#IPADDR=.\*\#IPADDR=10.0.0.200\#'

# 第19章  linux命令帮助

man  命令/配置文件

命令  --help

help  命令  （用于linux内置命令）

info  命令

搜索  linux  ls  命令

[http://man.linuxde.net/](http://man.linuxde.net/)

[http://linux.51yip.com/](http://linux.51yip.com/)

[http://www.shouce.ren/api/linux/\#](http://www.shouce.ren/api/linux/#)

# 第20章  常用快捷键

tab键   命令或路径补全功能

ctrl+c  终止当前命令或程序

ctrl+d  退出当前shell

ctrl+l  清屏

ctrl+a  命令行光标移到行首

ctrl+e  命令行光标移到行尾

ctrl+u  命令行删除光标到行首的内容

ctrl+k  命令行删除光标到行尾的内容

ctrl+r  命令行搜索

