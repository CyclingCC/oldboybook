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

绝对路径：从/\(根\)开始的路径

cat /etc/sysconfig/network-scripts/ifcfg-eth0

相对路径:不从/\(根\)开始

etc/sysconfig/network-scripts/

例子：

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



