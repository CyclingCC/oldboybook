#### 1、网卡的配置文件

\[root@oldboyedu42 ~\]\# \#/etc/sysconfig/网络-脚本/ifcfg-eth0

\[root@oldboyedu42 ~\]\# \#config

\[root@oldboyedu42 ~\]\# \#c  f g

\[root@oldboyedu42 ~\]\#  ll /etc/sysconfig/network-scripts/ifcfg-eth0

-rw-r--r--. 3 root root 229 Oct 16 16:55 /etc/sysconfig/network-scripts/ifcfg-eth0

#### 2、详细解释网卡的配置文件

\[root@oldboyedu42 ~\]\# cat /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0                         \#网卡的名字

HWADDR=00:0c:29:90:89:d9            \#HWADDR HardWare Address 硬件地址 MAC地址

TYPE=Ethernet                        \#网络类型  以太网

UUID=ae779ae6-044d-43d5-a33b-48c89e8de10e  \#UUID  唯一的标识 做到系统中独一无二。

ONBOOT=yes                   \#\*\*\*\*\*\*BOOT ON ? 在开机或重启网卡的时候是否启动网卡

NM\_CONTROLLED=yes                \#是否受network程序管理

BOOTPROTO=none              \#\*\*\*\*\*\*网卡是如何获取到ip地址 网卡获取ip地址的方式

\#dhcp    自动获取ip地址

\#none    固定的ip地址

\#static  固定的ip地址

IPADDR=10.0.0.100                          \#IPADDR ip地址

NETMASK=255.255.255.0                      \#子网掩码  决定这个局域网中最多有多少台机器

GATEWAY=10.0.0.2                           \#GATEWAY   网关 整个大楼的大门

DNS1=223.5.5.5

DNS2=223.6.6.6

USERCTL=no                                 \#普通用户是否能控制网卡

PEERDNS=yes                                \#网卡配置文件里面的DNS优先于/etc/resolv.conf

#### 练习题：

详细解释网卡配置文件中的每一行的含义？



