### 一、windows目录结构

##### windows  有几个分区  就有几个根

C:\Windows

D:\Program Files

E:\pycharm

F:\video

### 二、Unix目录发展

1969年，Ken Thompson 和 Dennis Ritchie 在小型机PDP-7上发明了Unix。1971年，他们将主机升级到PDP-11

当时，他们使用一种叫做RK05的存储盘，盘的容量大约是 1.5MB

![](/assets/8-1.png)

由于硬盘的容量很小，因此没过多久，操作系统存储盘数据（根目录）变得越来越大了，导致一块盘已经装不下数据了。于是，他们加上了第二块磁盘RK05，并且做了规定，第一块盘专门用来存放系统相关程序，第二块盘专门存放用户自己的程序，因此，挂载的目录取名为 /usr

也就是说，根目录  / 挂载在第一块盘， /usr 挂载在第二块盘。除此之外，两块盘里面的其它的目录结构是完全相同的

第一块盘   /bin  /sbin  /lib  /tmp

第二块盘  /usr/bin  /usr/sbin  /usr/lib   /usr/tmp

\[root@brj ~\]\# ls -ld /bin/ /sbin/ /tmp/ /usr/bin/ /usr/sbin/ /usr/tmp/

dr-xr-xr-x. 2 root root  4096 May  1 13:24 /bin/

dr-xr-xr-x. 2 root root 12288 May  1 13:24 /sbin/

drwxrwxrwt. 3 root root  4096 May  8 09:43 /tmp/

dr-xr-xr-x. 2 root root 28672 May  7 21:35 /usr/bin/

dr-xr-xr-x. 2 root root 12288 May  1 13:24 /usr/sbin/

drwxrwxrwt. 2 root root  4096 May  7 21:35 /usr/tmp/

### 三、linux目录

#### 1、linux目录机制

![](/assets/8-2.png)

![](/assets/8-3.png)

linux目录：一切从根开始， /  是所有目录的起点（顶点）： 相对路径和绝对路径

目录结构和设备是分离的，任何一个目录都可能对应一个不同的磁盘或分区

linux系统中不同的目录可以分布在不同的磁盘分区以及不同的磁盘上，windows系统中不同分区都是独立存在的

linux磁盘设备默认是无法访问的（黑屋子），没有窗户没有门。

开门开窗的过程就是 挂载，门窗就相当于目录，称为挂载点 /mnt

i、挂载的命令 mount

mount /dev/cdrom /mnt

ii、查看挂载情况：

df -h

cat /proc/mounts

iii、开机自动挂载：

/etc/fstab

#### 2、设备挂载与卸载

#### 挂载

\[root@oldboyedu36 ~\]\#

\[root@oldboyedu36 ~\]\# mount /dev/cdrom /mnt/

mount: block device /dev/sr0 is write-protected, mounting read-only

\[root@oldboyedu36 ~\]\# \#\#\#\#查看

\[root@oldboyedu36 ~\]\# df

Filesystem     1K-blocks    Used Available Use% Mounted on

/dev/sda3        9213440 1446572   7292196  17% /

tmpfs             953128       0    953128   0% /dev/shm

/dev/sda1         194241   40020    143981  22% /boot

/dev/sr0         3878870 3878870         0 100% /mnt

\[root@oldboyedu36 ~\]\# df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/sda3       8.8G  1.4G  7.0G  17% /

tmpfs           931M     0  931M   0% /dev/shm

/dev/sda1       190M   40M  141M  22% /boot

/dev/sr0        3.7G  3.7G     0 100% /mnt

\[root@oldboyedu36 ~\]\# cd /mnt/

\[root@oldboyedu36 mnt\]\# ls

CentOS\_BuildTag  isolinux                  RPM-GPG-KEY-CentOS-Debug-6

EFI              Packages                  RPM-GPG-KEY-CentOS-Security-6

EULA             RELEASE-NOTES-en-US.html  RPM-GPG-KEY-CentOS-Testing-6

GPL              repodata                  TRANS.TBL

images           RPM-GPG-KEY-CentOS-6

\[root@oldboyedu36 mnt\]\# ls -l

total 564

-r--r--r--. 2 root root     14 Mar 29 02:05 CentOS\_BuildTag

dr-xr-xr-x. 3 root root   2048 Mar 29 02:19 EFI

-r--r--r--. 2 root root    212 Nov 27  2013 EULA

-r--r--r--. 2 root root  18009 Nov 27  2013 GPL

dr-xr-xr-x. 3 root root   2048 Mar 29 02:24 images

dr-xr-xr-x. 2 root root   2048 Mar 29 02:19 isolinux

dr-xr-xr-x. 2 root root 534528 Mar 29 02:23 Packages

-r--r--r--. 2 root root   1359 Mar 28 23:53 RELEASE-NOTES-en-US.html

dr-xr-xr-x. 2 root root   4096 Mar 29 02:24 repodata

-r--r--r--. 2 root root   1706 Nov 27  2013 RPM-GPG-KEY-CentOS-6

-r--r--r--. 2 root root   1730 Nov 27  2013 RPM-GPG-KEY-CentOS-Debug-6

-r--r--r--. 2 root root   1730 Nov 27  2013 RPM-GPG-KEY-CentOS-Security-6

-r--r--r--. 2 root root   1734 Nov 27  2013 RPM-GPG-KEY-CentOS-Testing-6

-r--r--r--. 1 root root   3380 Mar 29 02:24 TRANS.TBL

#### 卸载

umount  /mnt 或 umount /dev/cdrom

#### 3、小结

i、一切从根开始，一切皆文件

ii、Linux下面的设备不挂载无法使用

iii、挂载===给设备开一个入口

iv、挂载点====设备的入口====目录

v、相对路径绝对路径

##### 提示：老男孩培训的学习思路，练习归纳总结的能力，把书由厚变薄（先总结然后再扩展）

#### 练习题：

1、linux的目录机制

2、设备如何挂载及卸载？



