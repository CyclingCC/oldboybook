# 第1章  windows目录结构

C:\Windows

D:\Program Files

E:\pycharm

F:\video

windows  有几个分区  就有几个根

# 第2章 unix目录发展

1969年，Ken Thompson 和 Dennis Ritchie 在小型机PDP-7上发明了Unix。1971年，他们将主机升级到PDP-11

当时，他们使用一种叫做RK05的存储盘，盘的容量大约是 1.5MB

# 第3章 linux目录结构

## 3.1 linux目录机制

linux目录：一切从根开始， /  是所有目录的起点（顶点）： 相对路径和绝对路径

倒挂的一棵树

目录结构和设备是分离的，任何一个目录都可能对应一个不同的磁盘或分区 

linux系统中不同的目录可以分布在不同的磁盘分区以及不同的磁盘上，windows系统中不同分区都是独立存在的



linux磁盘设备默认是无法访问的（黑屋子），没有窗户没有门。

开门开窗的过程就是 挂载

门窗就相当于目录，称为挂载点 /mnt

1.  挂载的命令 mount

        mount /dev/cdrom /mnt   

    2. 查看挂载情况：

        df -h

        cat /proc/mounts

     3. 开机自动挂载：    

         /etc/fstab

3.2  设备挂载与卸载

3.2.1  挂载

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

3.2.2  卸载

umount  /mnt

或

umount /dev/cdrom

