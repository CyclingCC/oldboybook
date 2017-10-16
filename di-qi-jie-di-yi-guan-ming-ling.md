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

