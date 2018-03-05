#### 1、linux系统用户分类

* 超级用户：UID为0代表root，皇帝linux管理员：root
* 普通用户：UID为500-655

  由超级用户或具备超级用户权限的用户创建的用户

* 虚拟用户：UID为1-499，存在满足文件或服务启动的需要。一般不能登录，只是傀儡

每个文件和进程/服务，都需要对应一个用户和用户组

用户和组的关系：

一对一，多对一，一对多，多对多

和用户关联的四个文件：

/etc/passwd /etc/shadow /etc/group /etc/gshadow

/etc/passwd（熟练，账户信息）

/etc/shadow /etc/group /etc/gshadow （创造一个索引（目录）软链接）

#### 2、passwd文件中一行的各个字段详细说明 {#passwd文件中一行的各个字段详细说明}

![](https://www.luffycity.com/linux-book/assets/tab19-19.png)

echo $SHELL

cat /etc/shells

#### 3、/etc/passwd 每一列的含义 {#111-etcpasswd-每一列的含义}

\[root@oldboyedu35-nb ~\]\# head -1 /etc/passwd

root:x:0:0:root:/root:/bin/bash

| root | :x | :0 | :0 | :root | :/root | :/bin/bash |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 账号名称 | ：账号密码 | ：账号UID | ：账号GID | ：用户说明 | ：用户家目录 | ：shell解释器（命令解释器） |

#### 4、小结论 {#112-小结论}

1、 useradd添加用户会更改/etc/passwd、/etc/shadow、/etc/group、/etc/gshadow

2、 passwd 为用户设置密码会更改/etc/shadow

\[root@oldboyedu35-nb ~\]\# ll /etc/passwd /etc/shadow /etc/group /etc/gshadow

-rw-r--r-- 1 root root 653 Mar 28 17:41 /etc/group

---------- 1 root root 531 Mar 28 17:41 /etc/gshadow

-rw-r--r-- 1 root root 1296 Mar 28 17:41 /etc/passwd

---------- 1 root root 1060 Mar 28 17:41 /etc/shadow

\[root@oldboyedu35-nb ~\]\# useradd alex888

\[root@oldboyedu35-nb ~\]\# ll /etc/passwd /etc/shadow /etc/group /etc/gshadow

-rw-r--r-- 1 root root 668 Apr 5 09:22 /etc/group

---------- 1 root root 543 Apr 5 09:22 /etc/gshadow

-rw-r--r-- 1 root root 1339 Apr 5 09:22 /etc/passwd

---------- 1 root root 1090 Apr 5 09:22 /etc/shadow

\[root@oldboyedu35-nb ~\]\# ll /etc/profile /etc/bashrc /root/.bash\_profile /root/.bashrc

-rw-r--r-- 1 root root 2695 Mar 21 12:42 /etc/bashrc \#别名

-rw-r--r-- 1 root root 1969 Mar 28 10:15 /etc/profile \#环境变量 别名

-rw-r--r--. 1 root root 176 May 20 2009 /root/.bash\_profile

-rw-r--r--. 1 root root 177 Mar 9 22:58 /root/.bashrc

\[root@oldboyedu35-nb ~\]\# ll -a /home/alex888/

total 20

drwx------ 2 alex888 alex888 4096 Apr 5 09:22 .

drwxr-xr-x. 9 root root 4096 Apr 5 09:22 ..

-rw-r--r-- 1 alex888 alex888 18 May 11 2016 .bash\_logout

-rw-r--r-- 1 alex888 alex888 176 May 11 2016 .bash\_profile

-rw-r--r-- 1 alex888 alex888 124 May 11 2016 .bashrc

####  {#113-与用户组相关的配置文件}

#### 6、回顾shell命令解释器 -/sbin/nologin {#114-回顾shell命令解释器--sbinnologin}

\[root@oldboyedu35-nb ~\]\# \#\#\#/sbin/nologin --- 让用户不能登陆 成为傀儡

\[root@oldboyedu35-nb ~\]\# su - daemon

This account is currently not available.

\[root@oldboyedu35-nb ~\]\# \#daemon:x:2:2:daemon:/sbin:/sbin/nologin

#### 练习题：

1、linux系统中有哪些个用户及用什么来区分的

2、passwd文件中其中一行每列的含义



