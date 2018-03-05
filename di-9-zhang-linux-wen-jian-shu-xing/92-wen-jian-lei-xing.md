### 一、文件的分类

f    file       普通文件

d    directory  目录

l    symlink  softlink   符号链接/软连接

#### 1、f    file       普通文件

1\).二进制文件-命令

2\).数据文件-data-只能通过指定的命令进行查看

3\).文本文件

\[root@oldboyedu42-lnb ~\]\# ls -l /etc/hosts  /bin/gawk  /tmp/etc.tar.gz

-rwxr-xr-x. 1 root root  382752 Nov 10  2015 /bin/gawk

-rw-r--r--. 2 root root     194 Oct 24 10:14 /etc/hosts

-rw-r--r--  1 root root 9735040 Nov 11 02:49 /tmp/etc.tar.gz

#### 2、查看文件类型

ls -l 文件名

扩展名:文件的小尾巴

.txt

.log

.conf

.sh    脚本

##### windows下扩展名: 用来给"系统"区分不同文件类型的。

##### linux下的扩展名：用来给"人类"区分不同文件类型的。

#### 练习题：

linux中的文件类型及如何查看

