#### 1、测试sudo

![](/assets/19-5.png)

echo "Defaults logfile=/var/log/sudo.log"&gt;&gt;/etc/sudoers

visudo -c

测试：root用户下

\[root@oldboyedu-35 tmp\]\# tailf /var/log/sudo.log

Apr 7 23:54:10 : oldboy : TTY=pts/1 ; PWD=/home/oldboy ; USER=root ;

COMMAND=list

Apr 8 00:24:36 : oldboy : command not allowed ; TTY=pts/1 ; PWD=/home/oldboy ;

USER=root ; COMMAND=/usr/bin/passwd root

测试：oldboy用户下

\[oldboy@oldboyedu-35 ~\]$ sudo passwd root

\[sudo\] password for oldboy:

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd root' as root on oldboyedu-35.

#### 2、sudo授权最小化 例题：给oldboy用户授权passwd命令，安全不能把皇帝推翻

第一个里程碑-不让修改root密码

oldboy ALL=\(ALL\) /usr/bin/passwd, ! /usr/bin/passwd root

oldboy用户:sudo passwd root XXXXX

oldboy： sudo passwd 如何限制？

解决方法：用户修改密码的时候 必须加上用户名

第二个里程碑-不让修改root sudo passwd

\#\#限制的方法 --用户修改密码的时候 必须加上用户名

oldboy ALL=\(ALL\) /usr/bin/passwd \[a-zA-Z0-9\]\*

第三个里程碑-彻底不让修改root密码

oldboy ALL=\(ALL\) /usr/bin/passwd \[a-zA-Z0-9\]\*, ! /usr/bin/passwd root

\[oldboy@oldboyedu-35 ~\]$ sudo passwd

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd' as root on oldboyedu-35.

\[oldboy@oldboyedu-35 ~\]$ sudo passwd root

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd root' as root on oldboyedu-35.

### 3、sudo权限集中管理项目

背景：root泛滥

\#第一个里程碑-演员--用户：

\#\#\#用户别名分类：

\#\#《用户必须存在》

\#\# 根据部门把用户分类---------用户别名

\#\#

\#\#\#\#把公司人员（需要使用服务器）分类

\#\#\#\#sa ----- system admin 系统管理员

User\_Alias KAIFA\_ADMINS = kaifa01, kaifa02

User\_Alias ADMINS = oldboy, oldgirl, %sa

User\_Alias NETADMINS = leo,maya

\#第二个里程碑-这些用户要干什么：

\#知道大家每个部门用的命令

\#命令分类

\#然后创建命令别名

Cmnd\_Alias USERCMD = /usr/sbin/useradd, /usr/sbin/userdel, /usr/bin/passwd , /bin/chown, /bin/chmod

Cmnd\_Alias DISKCMD = /sbin/fdisk, /sbin/parted

Cmnd\_Alias NETMAGCMD = /sbin/ifconfig, /etc/init.d/network

Cmnd\_Alias CTRLCMD = /usr/sbin/reboot, /usr/sbin/halt

Cmnd\_Alias LOOKCMD = /bin/grep, /usr/bin/tail, /bin/cat, /usr/bin/less

\#\#\#\#\#第三个里程碑---演戏---规划每个演员做什么动作 （每个用户执行什么命令）

开发人员： User\_Alias KAIFA\_ADMINS = kaifa01, kaifa02

```
        命令权限：LOOKCMD


        身份权限：root
```

运维人员： User\_Alias OLD\_ADMINS = oldboy, oldgirl, %sa

```
        命令权限：USERCMD, DISKCMD, NETMAGCMD, CTRLCMD, LOOKCMD


        身份权限：root
```

网络工程师：User\_Alias NETADMINS = leo,maya

```
        命令权限：NETMAGCMD


        身份权限：root
```

\#\#\#\#第四个里程碑-拍片

\#授权： 什么用户执行什么命令

\#root ALL=\(ALL\) ALL

\#用户 机器 角色 命令

KAIFA\_ADMINS ALL=\(root\) LOOKCMD

ADMINS ALL=\(root\) USERCMD, DISKCMD, NETMAGCMD, CTRLCMD, LOOKCMD

NETADMINS ALL=\(root\) NETMAGCMD

\#\#\#\#第五个里程碑-后期5毛钱特效--修改配置文件

\#\#\#快速命令

\#\#\#useradd

groupadd sa

useradd leo && echo 123\|passwd --stdin leo

useradd maya && echo 123\|passwd --stdin maya

useradd zuma && echo 123\|passwd --stdin zuma

useradd ett && echo 123\|passwd --stdin ett

useradd kaifa01 && echo 123\|passwd --stdin kaifa01

useradd kaifa02 && echo 123\|passwd --stdin kaifa02

\#\#\#user alias

User\_Alias KAIFA\_ADMINS = kaifa01, kaifa02

User\_Alias ADMINS = oldboy, oldgirl, %sa

User\_Alias NETADMINS = leo,maya

\#\#command alias

Cmnd\_Alias USERCMD = /usr/sbin/useradd, /usr/sbin/userdel, \

/usr/bin/passwd \[A-Za-z\]\*, /bin/chown, /bin/chmod

Cmnd\_Alias DISKCMD = /sbin/fdisk, /sbin/parted

Cmnd\_Alias NETMAGCMD = /sbin/ifconfig, /etc/init.d/network

Cmnd\_Alias CTRLCMD = /usr/sbin/reboot, /usr/sbin/halt

Cmnd\_Alias LOOKCMD = /bin/grep, /usr/bin/tail, /bin/cat, /usr/bin/less

\#\#rules

KAIFA\_ADMINS ALL=\(root\) LOOKCMD

ADMINS ALL=\(root\) USERCMD, DISKCMD, NETMAGCMD, CTRLCMD, LOOKCMD

NETADMINS ALL=\(root\) NETMAGCMD

\#\#\#\#第六个里程碑-试映---检查

1. 多开几个窗口--标记好了

2. 大象放冰箱-一步一步来

#### 4、sudo 配置文件/etc/sudoers 授权规则注意事项总结：

1） 授权规则中的所有ALL字符串必须为大写字母

2） 允许执行的命令是有顺序的。前面的为允许，后面的为禁止，执行命令的顺序是从后往前执行的

/usr/sbin/\*，/sbin/\*，！/usr/sbin/visudo,!/sbin/fdisk

再次强调，禁止的命令尽量放在后面

3） 一行内容超长可以用“\”反斜线换行

4） ！叹号表示非，就是命令取反的意思，即禁止执行的命令

5） 根据实际情况，来分类制作命令别名，用什么就给什么权限

