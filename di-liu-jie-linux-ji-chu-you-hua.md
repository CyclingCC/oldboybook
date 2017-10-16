# 第1章如何关闭一个软件/服务\(iptables\)

Linux一般作为服务用，但是很多时候我们希望访问服务器，如果某些访问被防火墙拦截的话就会访问不到。这个时候需要关闭防火墙来实现。还有一种是只有配置外网ip的linux服务器才需要开启防火墙，但即使是有外网ip，对于高并发高流量的业务服务器仍是不能打开的，因为会有较大性能损失，导致网站访问很慢，这种情况下只能在前端加更好的硬件防火墙了。

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
 2. 让他在开机不启动======&gt;chkconfigiptablesoff

