#### 1、主机名配置文件

\[root@brj ~\]\# cat /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=brj

#### 2、查看主机名

\[root@brj ~\]\# hostname

brj

#### 3、临时修改主机名

\[root@brj ~\]\# hostname oldboy36

#### 4、永久修改主机名

\[root@brj ~\]\# sed 's\#HOSTNAME=.\*\#HOSTNAME=oldboy36\#' /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=oldboy36

\[root@brj ~\]\# sed 's\#HOSTNAME=.\*\#HOSTNAME=oldboy36\#' /etc/sysconfig/network -i

\[root@brj ~\]\# cat /etc/sysconfig/network

NETWORKING=yes

HOSTNAME=oldboy36

#### 练习题：

说说如何修改主机名（分临时和永久）

