# 第1章 linux下重要目录

## 1.1  根目录  /

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

## 1.2 /bin目录

bin目录为常用二进制命令所在目录，比如ls、cp、mkdir、rm、cut等命令：/bin目录和/usr/bin类似。

## 1.3 /boot目录

boot目录是Linux 的内核及引导系统程序所需的文件目录。

## 1.4 /dev 目录

dev目录是设备文件目录，虚拟文件系统，主要存放所有系统中device的相关信息，不论是使用的或未使用的设备，只要有可能使用到，就会在/dev中建立一个相对应的设备文件；设备文件分为2种类型： 字符设备文件和块设备文件\(目录中基本上都是设备文件，如硬盘设备文件/dev/sda\)

重要子目录    解释说明

/dev/console    系统控制台，也就是直接和系统连接的监视器

/dev/hd    IDE设备文件

/dev/sd    sata、usb、scsi等设备文件

/dev/fd    软驱设备文件

/dev/tty    虚拟控制台设备文件

/dev/pty    提供远程虚拟控制台设备文件

/dev/null    所谓"黑洞"，所有写入该设备的信息都将消失，如当想要将屏幕上的输出信息隐藏起来时，只要将输出信息输入到/dev/null中即可

## 1.5 /etc 目录

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

## 1.6 /home目录

/home 是普通用户的家目录默认数据存放目录

## 1.7 /lib 目录

这个目录里存放着系统最基本的共享链接库和内核模块。共享链接库在功能上类似于Windows里的.dll文件

## 1.8 /lib64 目录

64位系统有这个文件夹，64位程序的库

## 1.9 /mnt 目录

临时用于挂载文件系统的地方。一般情况下这个目录是空的，而在我们将要挂载分区时在这个目录下建立目录，再将我们将要访问的设备挂载在这个目录上，这样我们就可访问文件了

## 1.10 /media 目录

可移动设备的挂载点，当前的操作系统通常会把U盘等设备自动挂载到该文件夹下

## 1.11 /lost+found 目录

这并不是Linux目录结构的组成部分，而是ext3文件系统用于保存丢失文件的地方。不恰当的关机操作和磁盘错误均会导致文件丢失，这意味着这些被标注为“在使用”，但却并未列于磁盘上的数据结构上。正常情况下，引导进程会运行fsck程序，该程序能发现这些文件。除了“/”分区上的这个目录外，在每个分区上均有一个lost+found目录。

## 1.12 /opt 目录

多数第三方软件默认安装到此位置

## 1.13 /proc目录

它是存在于内存中的虚拟文件系统。里面保存了内核和进程的状态信息。多为文本文件，可以直接查看

重要子目录    功能

/proc/version    存放内核版本

/proc/cpuinfo    处理器相关信息 top

/proc/meminfo    系统内存信息，free -m

/proc/loadavg    系统负载平均值信息uptime ,w

/proc/mounts    设备挂载信息，df -h

## 1.14 /root目录

/root目录是超级权限用户root的家目录

## 1.15 /sbin 目录

供超级用户使用的可执行文件，里面多是系统管理命令

## 1.16 /tmp 目录

该目录用以保存临时文件。该目录具有Sticky特殊权限，所有用户都可以在这个目录中创建、编辑文件。但只有文件拥有者才能删除文件

## 1.17 /usr目录

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

## 1.18 /var目录

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

## 1.19  目录层次标准FHS

[http://www.pathname.com/fhs/](http://www.pathname.com/fhs/)

ifdown  eth0  关闭网卡eth0

ifup    eth0   开启网卡eth0
