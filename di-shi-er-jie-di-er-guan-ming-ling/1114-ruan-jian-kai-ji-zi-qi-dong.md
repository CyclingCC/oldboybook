#### 装完 Centos 系统后，希望网络文件共享服务 NFS，仅在 3 级别上开机自启动，该如何做？

chkconfig --level 3 iptables on

chkconfig iptables on

#### 查看iptables开机启动状态

\[root@oldboy36 oldboy\]\# chkconfig --list iptables

iptables 0:off 1:off 2:off 3:off 4:off 5:off 6:off

\[root@oldboy36 oldboy\]\# chkconfig \|grep iptables

iptables 0:off 1:off 2:off 3:off 4:off 5:off 6:off

