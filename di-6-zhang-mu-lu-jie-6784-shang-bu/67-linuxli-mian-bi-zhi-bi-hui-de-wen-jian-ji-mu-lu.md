### 一、/etc目录下的重要文件

#### 1、/etc/sysconfig/network-scripts/ifcfg-eth0 网卡的配置文件

\[root@oldboy ~\]\# cat /etc/sysconfig/network-scripts/ifcfg-eth0 

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

#### 2、/etc/resolv.conf DNS的配置文件

* 修改DNS-在网卡中修改DNS-重启网卡
* 网卡配置文件的DNS优先于/etc/resolv.conf

##### 在Red Hat Enterprise Linux \(RHEL\)中配置DNS在哪里配置？

* 网卡配置文件 /etc/sysconfig/network-scripts/ifcfg-eth0
* /etc/resolv.conf

#### 3、/etc/sysconfig/network 修改主机名

linux如何修改主机名

##### i、临时-命令-重启服务器失效

\[root@oldboyedu42 ~\]\# hostname 

oldboyedu42

\[root@oldboyedu42 ~\]\# hostname  oldboyedu42-lnb

\[root@oldboyedu42 ~\]\# hostname 

oldboyedu42-lnb

##### ii、永久-重启服务器生效

\[root@oldboyedu42 ~\]\# cat /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=oldboyedu42-lnb

#### 4、/etc/hosts 解析主机名

ip地址与主机名的对应关系

程序代码--------&gt;测试环境10.0.0.200 

                  也要使用jd.com 

                  在测试电脑上使用jd.com 的时候 就相当于使用 10.0.0.200

10.0.0.200      jd.com 

\#通过修改/etc/hosts 让jd.com 解析到10.0.0.200 测试环境 

\[root@oldboyedu42-lnb oldboy\]\# cat /etc/hosts

127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4

::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

10.0.0.200  oldboyedu42-lnb  test01

\[root@oldboyedu42-lnb oldboy\]\# ping test01

PING oldboyedu42-lnb \(10.0.0.200\) 56\(84\) bytes of data.

64 bytes from oldboyedu42-lnb \(10.0.0.200\): icmp\_seq=1 ttl=64 time=0.052 ms

64 bytes from oldboyedu42-lnb \(10.0.0.200\): icmp\_seq=2 ttl=64 time=0.043 ms

64 bytes from oldboyedu42-lnb \(10.0.0.200\): icmp\_seq=3 ttl=64 time=0.041 ms

##### 小结:

i、主要是用来进行测试

10.0.0.200   www.jd.com 

ii、方便大家使用 

一眼能知道这个服务器干啥

test01 test01.oldboyedu.com





### 二、/usr目录下的重要文件

1、

2、

### 三、/var目录下的重要文件

1、

2、



### 四、/proc目录下的重要文件



