# 第1章  windows目录结构

C:\Windows

D:\Program Files

E:\pycharm

F:\video

windows  有几个分区  就有几个根

# 第2章 unix目录发展

1969年，Ken Thompson 和 Dennis Ritchie 在小型机PDP-7上发明了Unix。1971年，他们将主机升级到PDP-11

当时，他们使用一种叫做RK05的存储盘，盘的容量大约是 1.5MB

![](/assets/8-1.png)

# 第3章 linux目录结构

## 3.1 linux目录机制

![](/assets/8-2.png)

![](/assets/8-3.png)

linux目录：一切从根开始， /  是所有目录的起点（顶点）： 相对路径和绝对路径

倒挂的一棵树

目录结构和设备是分离的，任何一个目录都可能对应一个不同的磁盘或分区

linux系统中不同的目录可以分布在不同的磁盘分区以及不同的磁盘上，windows系统中不同分区都是独立存在的

linux磁盘设备默认是无法访问的（黑屋子），没有窗户没有门。

开门开窗的过程就是 挂载

门窗就相当于目录，称为挂载点 /mnt

1. 挂载的命令 mount

   mount /dev/cdrom /mnt

2. 查看挂载情况：

   df -h

   cat /proc/mounts

3. 开机自动挂载：

   /etc/fstab

## 3.2  设备挂载与卸载

### 3.2.1  挂载

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

### 3.2.2  卸载

umount  /mnt 或 umount /dev/cdrom

第4章 linux下重要目录

4.1  根目录  /

\[root@oldboy ~\]\# tree -L 1 /

/

├── bin      \#命令 二进制文件

├── boot     \#系统引导程序+内核

├── data

├── data1

├── dev      \#存放设备文件

├── etc       \#系统的配置文件

├── home     \#普通用户的家目录

├── lib       \#共享库文件

├── lib64     \#64位共享库文件

├── lost+found    文件系统损坏 临时文件位置

├── media

├── mnt          \#临时挂载点

├── oldgirl

├── opt          \#第三方程序存放位置

├── proc         \#虚拟的目录  内存中的信息映射到磁盘中

├── root         \#root用户家目录

├── sbin         \#超级命令  二进制文件

├── selinux       \#selinux及它的配置文件存放位置

├── srv

├── sys          \#虚拟的目录  内存中的信息

├── tmp         \#临时文件存放目录

├── usr          \#存放用户的程序

└── var          \#经常变化的文件（日志文件）存放目录

23 directories, 0 files

[http://edu.51cto.com/course/course\_id-5604.html](http://edu.51cto.com/course/course_id-5604.html)

总结：

1、linux系统的所有目录是一个有层次的倒着的树状目录结构，“/”根是所有目录的顶点

2、不同的目录数据可以跨越不同的磁盘分区或不同的磁盘设备

3、所有的目录都是按照一定的类别有规律的组织和命名的

相对路径：相对于当前路径下的路径

4.2 /bin目录

bin目录为常用二进制命令所在目录，比如ls、cp、mkdir、rm、cut等命令：/bin目录和/usr/bin类似。

4.3 /boot目录

boot目录是Linux 的内核及引导系统程序所需的文件目录。

4.4 /dev 目录

dev目录是设备文件目录，虚拟文件系统，主要存放所有系统中device的相关信息，不论是使用的或未使用的设备，只要有可能使用到，就会在/dev中建立一个相对应的设备文件；设备文件分为2种类型： 字符设备文件和块设备文件\(目录中基本上都是设备文件，如硬盘设备文件/dev/sda\)

重要子目录    解释说明

/dev/console    系统控制台，也就是直接和系统连接的监视器

/dev/hd    IDE设备文件

/dev/sd    sata、usb、scsi等设备文件

/dev/fd    软驱设备文件

/dev/tty    虚拟控制台设备文件

/dev/pty    提供远程虚拟控制台设备文件

/dev/null    所谓"黑洞"，所有写入该设备的信息都将消失，如当想要将屏幕上的输出信息隐藏起来时，只要将输出信息输入到/dev/null中即可

4.5 /etc 目录

/etc目录是系统和应用软件的配置文件的默认路径、服务启动命令的存放路径

重要目录    功能

/etc/motd    设置登录认证后的屏幕打印输出信息

/etc/sysconfig/network    可修改机器名及网卡启动，网关等配置，永久修改主机名需同时修改：/etc/sysconfig/network和hostname主机名

/etc/sysconfig/network-script/ifcfg-eth0    配置网络地址及网关、DNS\(网卡里配置DNS优先于在/etc/resolv.conf文件里配置\)

/etc/redhat-release    存储系统版本号信息文件

/etc/group    设定用户的组名与相关信息

/etc/passwd    系统中的用户描述信息，每行记录一个用户的信息

/etc/sudoers    可执行使用sudo命令配置文件（权限提升）

/etc/resolv.conf    设置linux本地客户端DNS的配置文件

/etc/hosts    设定用户ip与名字的对应解析表，相当于LAN局域网内的DNS

/etc/fstab    实现要开机挂载的文件系统的文件，若配置错误，则或导致服务器无法启动

/etc/init.d    存放通过yum或rpm 工具安装软件的默认启动程序的目录

/etc/profile    系统全局环境变量永久生效的配置文件

用户环境变量：~/.bash\_profile , ~/.bashrc

/etc/bashrc    专门用来设置别名

/etc/profile.d    加载系统登录程序目录，目录或文件独立存在

/etc/rc.local    用于存放开机自动启动程序命令（chkconfig常用来管理yum/rpm安装的程序服务的开机自启动,）

/etc/inittab    设定系统启动时init进程，设置系统runlevel运行级别及加载相关的级别对应自启动文件设置；linux开机启动流程

/etc/issue    存放登录见面信息显示内容

/etc/rsyslog.conf    系统日志配置

4.6 /home目录

/home 是普通用户的家目录默认数据存放目录

4.7 /lib 目录

这个目录里存放着系统最基本的共享链接库和内核模块。共享链接库在功能上类似于Windows里的.dll文件

4.8 /lib64 目录

64位系统有这个文件夹，64位程序的库

4.9 /mnt 目录

临时用于挂载文件系统的地方。一般情况下这个目录是空的，而在我们将要挂载分区时在这个目录下建立目录，再将我们将要访问的设备挂载在这个目录上，这样我们就可访问文件了

4.10 /media 目录

可移动设备的挂载点，当前的操作系统通常会把U盘等设备自动挂载到该文件夹下

4.11 /lost+found 目录

这并不是Linux目录结构的组成部分，而是ext3文件系统用于保存丢失文件的地方。不恰当的关机操作和磁盘错误均会导致文件丢失，这意味着这些被标注为“在使用”，但却并未列于磁盘上的数据结构上。正常情况下，引导进程会运行fsck程序，该程序能发现这些文件。除了“/”分区上的这个目录外，在每个分区上均有一个lost+found目录。

4.12 /opt 目录

多数第三方软件默认安装到此位置

4.13 /proc目录

它是存在于内存中的虚拟文件系统。里面保存了内核和进程的状态信息。多为文本文件，可以直接查看

重要子目录    功能

/proc/version    存放内核版本

/proc/cpuinfo    处理器相关信息 top

/proc/meminfo    系统内存信息，free -m

/proc/loadavg    系统负载平均值信息uptime ,w

/proc/mounts    设备挂载信息，df -h

4.14 /root目录

/root目录是超级权限用户root的家目录

4.15 /sbin 目录

供超级用户使用的可执行文件，里面多是系统管理命令

4.16 /tmp 目录

该目录用以保存临时文件。该目录具有Sticky特殊权限，所有用户都可以在这个目录中创建、编辑文件。但只有文件拥有者才能删除文件

4.17 /usr目录

/usr目录是系统存放用户程序，及数据，帮助文件等的目录

重要子目录    功能

/usr/lib    /usr/bin/和/usr/sbin/中二进制文件的库。

/usr/local    一般编译软件的时候默认路径\(如,yum或rpm安装包默认路径\)

/usr/bin    用户可执行文件目录

/usr/sbin    非必要的系统二进制文件，例如：大量网络服务的守护进程。

/usr/share    存放系统共用的东西，如帮助文件

/usr/src    源码程序存放目录

1. rpm –ivh 包名.rpm

2. yum install 包名

3. 源码\(./configure,make,make install\)定制

   /usr/include    存放C/C++头文件的目录

4.18 /var目录

/var目录是变量文件——在正常运行的系统中其内容不断变化的文件（动态的程序数据），如日志，脱机文件和临时电子邮件文件。

重要子目录    功能

/var/log/    各种系统日志文件存放地

/var/log/messages    系统信息默认日志文件，按周自动轮询

/var/log/secure    记录登录系统存取信息的文件，按周自动轮询

/var/spool/cron    定时任务配置文件路径

/var/spool/cron/root    root定时任务配置文件，默认按用户命名

/var/cache    应用程序的缓存文件

/var/lib    应用程序的信息、数据。如数据库的数据等都存放在此文件夹

/var/lock    锁文件

/var/run    正在执行着的程序的信息，如PID文件应存放于此

/var/tmp    临时文件

4.19  目录层次标准FHS

[http://www.pathname.com/fhs/](http://www.pathname.com/fhs/)

ifdown  eth0  关闭网卡eth0

ifup    eth0   开启网卡eth0

第5章  linux下重要文件

5.1  查看路由

\[root@oldboy ~\]\# route -n

Kernel IP routing table

Destination     Gateway         Genmask         Flags Metric Ref    Use Iface

10.0.0.0        0.0.0.0         255.255.255.0   U     0      0        0 eth0

169.254.0.0     0.0.0.0         255.255.0.0     U     1002   0        0 eth0

169.254.0.0     0.0.0.0         255.255.0.0     U     1003   0        0 eth1

0.0.0.0         10.0.0.2        0.0.0.0         UG    0      0        0 eth0

5.2  DNS配置文件

\[root@oldboy ~\]\# cat /etc/resolv.conf

; generated by /sbin/dhclient-script

search localdomain

nameserver 10.0.0.2

网卡里面配置DNS优先

5.3  网卡配置文件

cat /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0

TYPE=Ethernet

ONBOOT=yes

NM\_CONTROLLED=yes

BOOTPROTO=static

NETMASK=255.255.255.0

IPADDR=10.0.0.9

GATEWAY=10.0.0.2

5.4  hosts文件

\[root@oldboy ~\]\# cat /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4

::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

5.5  hosts文件在企业中的作用

1、开发，产品，测试等人员，用于通过正式的域名测试产品

2、服务器之间调用可以用域名（内部DNS），方便迁移

5.6  主机名配置  /etc/sysconfig/network

\[root@brj ~\]\# cat /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=brj

5.7  查看主机名

\[root@brj ~\]\# hostname

brj

5.8  临时修改主机名

\[root@brj ~\]\# hostname oldboy36

5.9  永久修改主机名

\[root@brj ~\]\# sed 's\#HOSTNAME=.\*\#HOSTNAME=oldboy36\#' /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=oldboy36

\[root@brj ~\]\# sed 's\#HOSTNAME=.\*\#HOSTNAME=oldboy36\#' /etc/sysconfig/network -i

\[root@brj ~\]\# cat /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=oldboy36

5.10  开机自动挂载

\[root@oldboy ~\]\# cat /etc/fstab

\#

\# /etc/fstab

\# Created by anaconda on Sun Mar  6 16:23:29 2016

\#

\# Accessible filesystems, by reference, are maintained under '/dev/disk'

\# See man pages fstab\(5\), findfs\(8\), mount\(8\) and/or blkid\(8\) for more info

\#

UUID=fdd03bd8-212a-4e29-8be1-817dcfc0edcc /                       ext4    defaults        1 1

UUID=6d167fb4-7536-4076-b7be-9530cb88fee1 /boot                   ext4    defaults        1 2

UUID=848f0d7b-e66d-43e1-a9a9-e126657fcbab swap                    swap    defaults        0 0

tmpfs                   /dev/shm                tmpfs   defaults        0 0

devpts                  /dev/pts                devpts  gid=5,mode=620  0 0

sysfs                   /sys                    sysfs   defaults        0 0

proc                    /proc                   proc    defaults        0 0

5.11  开机自动启动程序

/etc/rc.local

5.12  系统运行级别

\[root@oldboy36 ~\]\# cat /etc/inittab

\# inittab is only used by upstart for the default runlevel.

\#

\# ADDING OTHER CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.

\#

\# System initialization is started by /etc/init/rcS.conf

\#

\# Individual runlevels are started by /etc/init/rc.conf

\#

\# Ctrl-Alt-Delete is handled by /etc/init/control-alt-delete.conf

\#

\# Terminal gettys are handled by /etc/init/tty.conf and /etc/init/serial.conf,

\# with configuration in /etc/sysconfig/init.

\#

\# For information on how to write upstart event handlers, or how

\# upstart works, see init\(5\), init\(8\), and initctl\(8\).

\#

\# Default runlevel. The runlevels used are:

\#   0 - halt \(Do NOT set initdefault to this\)

\#   1 - Single user mode

\#   2 - Multiuser, without NFS \(The same as 3, if you do not have networking\)

\#   3 - Full multiuser mode

\#   4 - unused

\#   5 - X11

\#   6 - reboot \(Do NOT set initdefault to this\)

\#

id:3:initdefault:

5.13  查看当前运行级别

\[root@oldboy36 ~\]\# runlevel

N 3

5.14  切换运行级别

\[root@oldboy36 ~\]\# init 2

\[root@oldgirl ~\]\# ll /etc/rc.d/

init.d/     rc0.d/      rc2.d/      rc4.d/      rc6.d/      rc.sysinit

rc          rc1.d/      rc3.d/      rc5.d/      rc.local

\[root@oldgirl ~\]\# ll /etc/rc.d/

总用量 60

drwxr-xr-x. 2 root root  4096 3月   6 16:26 init.d

-rwxr-xr-x. 1 root root  2617 7月  24 2015 rc

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc0.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc1.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc2.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc3.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc4.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc5.d

drwxr-xr-x. 2 root root  4096 3月  13 21:02 rc6.d

-rwxr-xr-x. 1 root root   220 7月  24 2015 rc.local

-rwxr-xr-x. 1 root root 20097 7月  24 2015 rc.sysinit

\[root@oldgirl ~\]\# ll /etc/rc.d/rc3.d/

总用量 0

lrwxrwxrwx. 1 root root 16 3月   6 16:26 K01smartd -&gt; ../init.d/smartd

5.15   服务管理程序目录  /etc/init.d/

\[root@oldboy36 ~\]\# /etc/init.d/iptables status

iptables: Firewall is not running.

\[root@oldboy36 ~\]\# /etc/init.d/iptables stop

5.16  环境变量配置文件

/etc/profile

/etc/profile.d/\*.sh

~/ .bash\_profile

~/ .bashrc

/etc/bashrc

5.17  系统登录提示信息

/etc/issue      认证前的输出信息，默认输出版本内核信息

/etc/issue.net

/etc/motd    设置认证后的输出信息

5.18  系统日志文件

/var/log/messages

dmseg 命令可以查看系统故障信息（/var/log/dmesg） 依赖于rsyslog服务开启

轮询日志由 /etc/logrotate.conf  和  /etc/logrotate.d/syslog 控制

/var/log/secure    记录登入系统存取信息的文件，按周自动轮询，例如 pop3,ssh,telnet,ftp 等都会记录在此。  系统安全的日志文件，依赖于rsyslog服务

/var/log/messages    系统默认的日志文件  每周自动切割一次

/var/log/wtmp    记录登录者信息的文件

/var/spool/cron/root    定时任务配置文件

/proc/cpuinfo    关于处理器的信息，如类型、厂家、型号和性能等  top 看cpu  sar

/proc/meminfo    系统内存信息， free -m

/proc/devices    当前运行内核所配置的所有设备清单

/proc/dma    当前正在使用的DMA通道

/proc/filesystems    当前运行内核所配置的文件系统

/proc/interrupts    正在使用的中断，和曾经有多少个中断

/proc/ioports    当前正在使用的I/O端口

/proc/loadavg    系统负载平均值信息（系统的繁忙情况，比较准确，但是不够细致系统性能指标），uptime的结果   负载值不要超过CPU的核数  看负载 top  uptime

/proc/mounts    设备的挂载信息，  df  -h 类似

5.19  必须要掌握的重要目录文件

/etc/sysconfig/network-scripts/ifcfg-eth0

/etc/resolv.conf

/etc/hosts

/etc/sysconfig/network

/etc/fstab

/etc/rc.local

/etc/inittab

/etc/init.d

/etc/profile 全局（所有用户）

/etc/bashrc  全局（所有用户）

~/.bashrc    局部（当前用户）

/usr/local

/usr/src

/var/log/messages

/var/log/secure

/proc/cpuinfo

/proc/meminfo

/proc/loadavg

/proc/mounts

[http://yangrong.blog.51cto.com/6945369/1288072](http://yangrong.blog.51cto.com/6945369/1288072)

第6章 目录详解

/      处于linux系统树形结构的最顶端，它是linux文件系统的入口，所有的目录、文件、设备都在/之下。

/bin   bin是Binary的缩写，存放着linux系统命令。

/dev   dev是Device的缩写。存放的是linux的外部设备，在linux中访问设备的方式和访问文件的方式是相同的。（注意：设备文件不是驱动程序。过去，在添加新磁盘或设备后，往往需要手动增加设备文件。现在通常我们不需要手动增加设备文件，运行一下service kudzu start ，系统就会自动配置相应的设备。）

/home  用户的主目录。在liunx系统中，每个用户都有一个自己的目录，一般该目录名是以用户的帐号命名的。

/lib   这个目录里存放着系统最基本的动态链接共享库，包含许多被/bin/和/sbin/中的程序使用的库文件，目录/usr/lib/中含有更多用于用户程序的库文件。作用类似于windows里的DLL文件，几乎所有的应用程序都需要用到这些共享库。

/media  linux系统自动识别的一些设备，例如U盘、光驱、移动硬盘等，linux会把识别的设备挂载到这个目录下。

/mnt   系统提供该目录是为了让用户临时挂载别的文件系统的，可以将光驱挂载到/mnt/上，然后进入该目录就可以查看光驱里的内容。

/opt   主机额外安装软件所摆放的目录。默认是空的。

/root  这个不用介绍了吧，呵呵。超级管理员的用户主目录。

/selinux  这个目录是RedHat/CentOS所特有的目录，Selinux是一个安全机制，这个比较复杂，这个目录就是存放Selinux相关的文件的，一般我们安装操作系统的时候禁止使用它。

/sys   这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统sysfs，sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统。该文件系统是内核设备树的一个直观反映。该文件系统是内核设备树的一个直观反映。当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统种被创建。

/usr   包括与系统用户直接有关的文件和目录，例如应用程序及支持它们的库文件。类似于windows下的program files目录。

/boot  包括内核和其它系统启动期间使用的文件。是启动linux时使用的核心文件，有连接文件和镜像文件。

/etc   存放系统配置文件和目录，非常重要，经常会用到它，要牢记。

/lost+found  默认为空，被FSCK（file system check用来检查和维护不一致的文件系统。若系统掉电或磁盘发生问题，可利用fsck命令对文件系统进行检查）用来放置零散文件（没有名称的文件）。当系统非法关机后，这里就会存放一些文件。

/misc   存放杂项文件或目录，即那些用途或含义不明确的文件或目录可以存放在该目录下。

/proc    操作系统运行时，进程（正在运行中的程序）信息及内核信息（比如cpu、硬盘分区、内存信息等）存放在这里。/proc目录是伪装的文件系统proc的挂载目录，proc并不是真正的文件系统。因此，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。也就是说，这个目录的内容不在硬盘上而是在内存里。

/sbin  大多数涉及系统管理的命令都存放在该目录中，它是超级权限用户root的可执行命令存放地，普通用户无权限执行这个目录下的命令，凡是目录sbin中包含的命令都是root权限才能执行的。

/srv    该目录存放一些服务启动之后需要提取的数据。

/tmp    该目录用于存放临时文件，有时用户运行程序的时候，会产生一些临时文件。/tmp就是用来存放临时文件的。/var/tmp目录和该目录的作用是相似的。

/var    该目录的内容是经常变动的，/var下有/var/log目录用来存放系统日志的目录。/var/www目录用来定义Apache服务器站点存放目录。/var/lib用来存放一些库文件。

=======================================================================

/usr/bin   这个目录是可执行程序的目录，普通用户就有权限执行。当我们从系统自带的软件包安装一个程序时，他的可执行文件大多会放在这个目录。相似的目录是/usr/local/bin目录。有时/usr/bin中的文件是/usr/local/bin的链接文件。

/usr/sbin  这个目录也是可执行程序的目录，但大多存放涉及系统管理的命令。只有root权限才能执行，相似目录是/sbin或/usr/local/sbin或/usr/X11R6/sbin等。

/usr/src   内核源码默认的放置目录

/proc/cpuinfo  关于处理器的信息，如类似、厂家、型号和性能等。比如cat /proc/cpuinfo

/proc/devices  当前运行内核所配置的所有设备清单。

/proc/filesystems   当前运行内核所配置的文件系统。

/proc/dma 当前正在使用的DMA通道。

/proc/interrupts 正在使用的中断和曾经有多少个中断。

/proc/ioports 当前正在使用的I/O端口。

/etc/init.d 这个目录是用来存放系统或服务器以System V模式启动的脚本，这在以System V模式启动或初始化的系统中常见。比如RedHat Fedora。

/etc/xinetd.d 如果服务器是通过xinetd模式运行的，它的脚本要放在这个目录下。有些系统没有这个目录，比如Slackware，有些老的版本也没有。在Redhat Fedora中比较新的版本中存在。

/etc/rc.d 这是Slackware发行版中有的一个目录，是BSD方式启动脚本的存放地，比如定义网卡，服务器开启脚本等。

/etc/X11 是X-Window相关的配置文件存放地。

/usr/local 这个目录一般是用来存放用户自编译安装软件的存放目录。一般是通过源码包安装的软件，如果没有特别指定安装目录的话，一般是安装在这个目录中。

/usr/lib 该目录和/lib目录相似，是库文件的存储目录。存放一些常用的共享库。

/usr/share 该目录用于存放系统共用的东西，比如/usr/share/fonts是字体目录，是用户都共用的。

/usr/share/doc 该目录是Linux共享文档的存放地。

/usr/share/man 该目录是共享的帮助文件的存放地。

/var/adm 比如软件包安装信息、日志、管理信息等就存放在该目录下，在Slackware操作系统中是有这个目录的。在Fedora中好象没有。

/var/log 该目录用于存放系统日志。

/var/spool 打印机、邮件、代理服务器等假脱机目录存放在该目录下。

# 

# 



