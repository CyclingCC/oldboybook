#### linux 系统运行级别一般为 0-6，请分别写出每个级别的含义

#### 运行级别 {#1511--运行级别}

0 - 停止

1 - 单用户模式

2 - 多用户，无NFS

3 - 完全多用户模式

4 - 未使用

5 - X11（图形模式）

6 - 重新启动

#### 系统运行级别配置文件 {#1512--系统运行级别配置文件}

/etc/inittab

id:3:initdefault:

#### 查看运行级别 {#1513--查看运行级别}

\[root@oldboy36 oldboy\]\# runlevel

N 3

#### 切换运行级别 {#1514--切换运行级别}

\[root@oldboy36 oldboy\]\# init 2

\[root@oldboy36 oldboy\]\# runlevel

3 2

