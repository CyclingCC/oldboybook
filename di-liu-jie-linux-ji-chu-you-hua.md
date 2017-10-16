# 第1章 如何关闭一个软件/服务\(iptables\)

Linux一般作为服务用，但是很多时候我们希望访问服务器，如果某些访问被防火墙拦截的话就会访问不到。这个时候需要关闭防火墙来实现。还有一种是只有配置外网ip的linux服务器才需要开启防火墙，但即使是有外网ip，对于高并发高流量的业务服务器仍是不能打开的，因为会有较大性能损失，导致网站访问很慢，这种情况下只能在前端加更好的硬件防火墙了。

![](/assets/6-1.png)

## 1.1关闭正在运行的iptables

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables start开启防火墙

iptables: Applying firewall rules: \[ OK \]

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables stop关闭防火墙

iptables: Setting chains to policy ACCEPT: filter \[ OK \]

iptables: Flushing firewall rules: \[ OK \]

iptables: Unloading modules: \[ OK \]

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables stop注意：为了保证防火墙真的关闭了，需要执行两次

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables status查看防火墙的状态

iptables: Firewall is not running.

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables restart重新启动防火墙

iptables: Applying firewall rules: \[ OK \]

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables restatus提醒自己一下，看看后边可以跟的命令

Usage: iptables {start\|stop\|reload\|restart\|condrestart\|status\|panic\|save}

## 1.2开机自启动\(不让它下次开机时启动的设置\)

重启后生效，不会影响当前正在运行的软件

chkconfig 查看状态linux管理开机自启动软件（服务）===chkconfig --list

chkconfig iptables off 关闭

chkconfig iptables on 开启

## 1.3检查结果是否正在运行\(防火墙和开机自启动\)

说明：管理开机启动项目===&gt;重启后生效 不能管理正在运行的服务

管理开启自动启动的服务

重启后生效

不会影响当前正在运行的服务

### 1.3.1查看防火墙的状态

\[root@oldboy35-moban ~\]\# /etc/init.d/iptables status

iptables: Firewall is not running.

### 1.3.2查看防火墙开机自启动的状态

法一：

\[root@oldboy35-moban ~\]\# chkconfig \|grep ipt

iptables 0:off 1:off 2:off 3:off 4:off 5:off 6:off

法二：

\[root@oldboy35-moban ~\]\# chkconfig --list iptables

iptables 0:off 1:off 2:off 3:off 4:off 5:off 6:off

## 1.4小结：彻底的让一个服务，不再运行

1. 关闭当前正在运行的进程（服务）=====&gt;/etc/init.d/iptablesstop  
   1. 让他在开机不启动======&gt;chkconfigiptablesoff

# 第2章 字符集修改过程

什么是字符集？

字符集是一套文字字符号及其编码。目前linux常用的字符集有：

1）GBK：定长，双字节，不是国际标准，支持的系统不少，实际企业用的不多

2）UTF-8：非定长，1~4字节，广泛支持，MYSQL也使用UTF-8，企业广泛使用

![](/assets/6-2.png)

提示：

乱码的核心解决方法：

1.系统字符集\(utf-8\)

2.xshell软件的字符集保持一致\(utf-8\)

3.文件使用的字符集一致

zh\_CN.GBK

注意“zh\_CN.UTF-8”的大小写字母

这个中文显示配置要跟自己的xshell客户端的配置一致

## 2.1 查看系统当前的字符集

\[root@oldboy35-moban ~\]\# echo $LANG

en\_US.UTF-8

## 2.2 系统字符集配置文件的位置

\[root@oldboy35-moban ~\]\# cat /etc/sysconfig/i18n

LANG="en\_US.UTF-8"

SYSFONT="latarcyrheb-sun16"

## 2.3 备份

\[root@oldboy35-moban ~\]\# cp /etc/sysconfig/i18n /etc/sysconfig/i18n.bak

## 2.4 修改配置文件

法一：\[root@oldboy35-moban ~\]\# echo 'LANG="zh\_CN.UTF-8"' &gt;/etc/sysconfig/i18n

法二：\[root@oldboy35-moban ~\]\# vi /etc/sysconfig/i18n 添加LANG="zh\_CN.UTF-8"内容

## 2.5 让配置文件生效

\[root@oldboy35-moban ~\]\# source /etc/sysconfig/i18n 使上文修改生效

## 2.6 查看系统当前的字符

\[root@oldboy35-moban ~\]\# echo＄LANG

\[root@oldboy35-moban ~\]\# echo $LANG

zh\_CN.UTF-8

## 2.7 恢复原有英文环境

\[root@oldboy35-moban ~\]\# \cp /etc/sysconfig/i18n.bak /etc/sysconfig/i18n

\[root@oldboy35-moban ~\]\# source /etc/sysconfig/i18n

\[root@oldboy35-moban ~\]\# echo $LANG

en\_US.UTF-8

## 2.8 小结

如果乱码了，解决方法：

1.命令临时修改字符集

export LANG=en\_US.UTF-8

2.写入到合同里面

cp /etc/sysconfig/i18n /etc/sysconfig/i18n.bak

echo 'LANG=en\_US.UTF-8' &gt;/etc/sysconfig/i18n

3.让他生效

source /etc/sysconfig/i18n

4.检查

# 第3章 selinux关闭

## 3.1 selinux介绍

SELinux\(Security-EnhancedLinux\)是美国国家安全局（NSA）对于[强制](http://baike.so.com/doc/6296629.html)访问控制的实现，是Linux®上最杰出的新安全子[系统](http://baike.so.com/doc/5402991.html)。NSA是在Linux社区的帮助下开发了一种访问控制体系，在这种访问控制体系的限制下，进程只能访问那些在他的任务中所需要文件。

两种方法关闭：

1. 一种是临时关闭法
2. 一种是永久关闭法

## 3.2 临时关闭法

\#数字0表示Permissive，即给出警告提示，但不会阻止操作，相当于disabled。  
 \#数字1表示Enforcing，即表示SElinux为开启状态。

getenforce查看selinux的状态

\#\#\#命令行临时  
 \[root@oldboyedu-35~\]\#getenforce  
 Enforcing  
 \[root@oldboyedu-35~\]\#setenforce  
 usage:setenforce\[Enforcing\|Permissive\|1\|0\]  
 \[root@oldboyedu-35~\]\#setenforce0  
 \[root@oldboyedu-35~\]\#getenforce  
 Permissive

提示：修改配置SElinux后，要想使其生效，必须要重启系统，因此，可配合使用setenfore 0时使其关闭的命令，这样在重启前后都可以使得SElinux关闭生效了，也就是说无需立刻重新启动了，在生成场景下linux机器是不能随意重启的\(不要给自己找任何理由重启\)

## 3.3 永久关闭法

\#\#\#文件中更改，永久生效

第一步操作前的备份\(复制\)：

\[root@oldboy35-moban ~\]\# cp /etc/selinux/config /etc/selinux/config.bak

第二步cat看一眼 找目标

\[root@oldboy35-moban ~\]\# cat /etc/selinux/config

\[root@oldboy35-moban ~\]\# sed 's\#SELINUX=enforcing\#SELINUX=disabled\#g' /etc/selinux/config

第三步 成功后加-i替换

\[root@oldboy35-moban ~\]\# sed -i 's\#SELINUX=enforcing\#SELINUX=disabled\#g' /etc/selinux/config

第四步 查看

\[root@oldboyedu-35~\]\#grep"=disabled"/etc/selinux/config  
 SELINUX=disabled

\[root@oldboy35-moban ~\]\# cat /etc/selinux/config

## 3.4  更改文件的规范

1. 将要修改的文件做备份\(cat,cp,sed -i .bak\)
2. cat看一眼，找下目标文件
3. 用sed 's\#\#\#g' 在命令行中显示出替换后的内容
4. 执行成功了，在加 -i 参数
5. 再查看改过后的内容，cat/grep

## 3.5 小结

1.操作前要备份

2.cat看下内容，找下目标

3.sed 's\#\#\#g' 查找下内容

4.成功找出目标后，加上-i参数

5.再次用cat查看，更改后的状态

###### 


