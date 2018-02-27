#### 1、inode

##### 1\)怎么来的

格式化创建文件系统的时候诞生的。

##### 2\)啥意思

index node 索引节点

inode是用来存放文件的属性信息，block的位置

inode号码（数字）

##### 3\)特点

  1\#linux里面创建一个非空文件要占用一个inode和至少1个block

##### 4\)查看 

\[root@oldboyedu44 ~\]\# ls -lhi /etc/hosts

915740 -rw-r--r--. 2 root root 158 Jan  8  2018 /etc/hosts

##### \#系统中inode一共有多少 用了多少

创建一个文件会减少一个inode

\[root@oldboyedu44 ~\]\# df -i

Filesystem      Inodes   IUsed   IFree IUse% Mounted on

/dev/sda3      1250928  55504 1195424    5% /

tmpfs           125514     1  125513    1% /dev/shm

/dev/sda1        51200    38   51162    1% /boot

#### 2、block

##### 1\)怎么来的

格式化创建文件系统的时候诞生的。

##### 2\)啥意思

实际用来存放数据的地方

##### 3\)特点 

  1\#存放数据的

  2\#block的大小默认4KB \(centos 6.x\)

  3\#文件比较大，需要使用多个block；文件比较小的时候（1KB）剩余的空间会被浪费。

##### 4\)查看

  \#查看 系统中block的使用情况=====磁盘空间的使用情况

\[root@oldboyedu42-lnb ~\]\# df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/sda3       8.8G  1.5G  6.9G  18% /

tmpfs           931M     0  931M   0% /dev/shm

/dev/sda1       190M   40M  141M  22% /boot

##### inode的个数

\[root@oldboyedu42-lnb ~\]\# \#grep 过滤 不区分大小写

\[root@oldboyedu42-lnb ~\]\# dumpe2fs /dev/sda3 \|grep -i "inode size"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode size:	          256

