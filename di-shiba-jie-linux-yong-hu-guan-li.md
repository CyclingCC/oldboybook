# 第1章 linux用户管理

### 1.1 linux系统用户分类

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

#### passwd文件中一行的各个字段详细说明

![](/assets/tab19-19.png)

echo $SHELL

cat /etc/shells

#### 1.1.1 /etc/passwd 每一列的含义

\[root@oldboyedu35-nb ~\]\# head -1 /etc/passwd

root:x:0:0:root:/root:/bin/bash

| root | :x | :0 | :0 | :root | :/root | :/bin/bash |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 账号名称 | ：账号密码 | ：账号UID | ：账号GID | ：用户说明 | ：用户家目录 | ：shell解释器（命令解释器） |

#### 1.1.2 小结论

1、    useradd添加用户会更改/etc/passwd、/etc/shadow、/etc/group、/etc/gshadow

2、    passwd 为用户设置密码会更改/etc/shadow

\[root@oldboyedu35-nb ~\]\# ll /etc/passwd /etc/shadow /etc/group /etc/gshadow

-rw-r--r-- 1 root root  653 Mar 28 17:41 /etc/group

---------- 1 root root  531 Mar 28 17:41 /etc/gshadow

-rw-r--r-- 1 root root 1296 Mar 28 17:41 /etc/passwd

---------- 1 root root 1060 Mar 28 17:41 /etc/shadow

\[root@oldboyedu35-nb ~\]\# useradd alex888

\[root@oldboyedu35-nb ~\]\# ll /etc/passwd /etc/shadow /etc/group /etc/gshadow

-rw-r--r-- 1 root root  668 Apr  5 09:22 /etc/group

---------- 1 root root  543 Apr  5 09:22 /etc/gshadow

-rw-r--r-- 1 root root 1339 Apr  5 09:22 /etc/passwd

---------- 1 root root 1090 Apr  5 09:22 /etc/shadow

\[root@oldboyedu35-nb ~\]\# ll /etc/profile /etc/bashrc  /root/.bash\_profile  /root/.bashrc

-rw-r--r--  1 root root 2695 Mar 21 12:42 /etc/bashrc   \#别名

-rw-r--r--  1 root root 1969 Mar 28 10:15 /etc/profile  \#环境变量 别名

-rw-r--r--. 1 root root  176 May 20  2009 /root/.bash\_profile

-rw-r--r--. 1 root root  177 Mar  9 22:58 /root/.bashrc

\[root@oldboyedu35-nb ~\]\# ll -a  /home/alex888/

total 20

drwx------  2 alex888 alex888 4096 Apr  5 09:22 .

drwxr-xr-x. 9 root    root    4096 Apr  5 09:22 ..

-rw-r--r--  1 alex888 alex888   18 May 11  2016 .bash\_logout

-rw-r--r--  1 alex888 alex888  176 May 11  2016 .bash\_profile

-rw-r--r--  1 alex888 alex888  124 May 11  2016 .bashrc

#### 1.1.3 与用户组相关的配置文件

/etc/group     \#--&gt;用户组配置文件

/etc/gshadow  \#--&gt;用户组的影子文件

#### 1.1.4 回顾shell命令解释器 -/sbin/nologin

\[root@oldboyedu35-nb ~\]\# \#\#\#/sbin/nologin   --- 让用户不能登陆  成为傀儡

\[root@oldboyedu35-nb ~\]\# su - daemon

This account is currently not available.

\[root@oldboyedu35-nb ~\]\# \#daemon:x:2:2:daemon:/sbin:/sbin/nologin

### 1.2 linux用户管理命令

#### 1.2.1 管理用户命令汇总

| 命令 | 注释说明 |
| :--- | :--- |
| useradd增 | \#--&gt;※同adduser命令，执行此命令可在系统中添加用户（更改四个用户文件） |
| userdel删 | 执行此命令可删除用户及相关用户的配置或文件（更改四个用户文件） |
| passwd | \#--&gt;※执行此命令可为用户设置或修改密码。更改/etc/shadow文件 |
| change | 修改用户密码属性。管理/etc/shadow文件 |
| usermod修改 | \#--&gt;※修改用户信息的命令，可以通过usermod来修改登录名、用户的家目录等等 |
| id查 | \#--&gt;※查看用户的UID、GID及所归属的用户组 |
| su | \#--&gt;※用户角色切换工具。su - |
| sudo | \#--&gt;※sudo是通过另一个用户来执行命令（execute a command as another user）,su是用来切换用户，然后通过切换到的用户来完成相应的任务，但sudo能在命令后面直接跟命令执行，比如sudo ls /root，不需要root密码就可以执行只有root才能执行相应的命令。或具备的目录权限；这个权限需要通过visudo命令或直接编辑/etc/sudoers来实现 |
| visudo | \#--&gt;※visudo配置sudo权限的编辑命令；也可以不用这个命令，直接用vi来编辑/etc/sudoers实现。但推荐用visudo来操作（会自动检查语法） |

#### 1.2.2 管理用户组命令汇总

| 命令 | 注释说明 |
| :--- | :--- |
| groupadd | \#--&gt;※添加用户组 |
| groupdel | 删除用户组 |
| groupmod | 修改用户组信息 |
| gpasswd | 为用户组设置密码 |
| groups | 显示用户所属的用户组 |
| newgrp | 更改用户所属的有效用户组 |

#### 1.2.3 /etc/skel目录

新用户的老家的默认的样子，从/etc/skel目录复制过来

/etc/skel 目录是用来存放新用户环境变量文件的目录，当我们添加新用户时，这个目录下的所有文件会自动被复制到新添加的用户的家目录下

默认情况下，/etc/skel 目录下的所有文件都是隐藏文件（以点开头的文件）;通过修改、添加、删除/etc/skel目录下的文件，我们可为新创建的用户提供统一的、标准的、初始化用户环境（给所有新用户的一个家默认样子）

#### 1.2.4 企业面试案例】：请问如下登录环境故障的原理及解决办法？

-bash-4.1$

-bash-4.1$

假设切换到alex888

-bash-4.1$

-bash-4.1$

\[alex888@oldboyedu35-nb ~\]$

\[alex888@oldboyedu35-nb ~\]$

第一个里程碑-模拟环境

useradd alex888

su - alex888

whoami

\rm -f .bash\*

第二个里程碑-xshell新建一个窗口-并切换到alex888用户

\[root@oldboyedu35-nb ~\]\# su - alex888

-bash-4.1$ whoami

alex888

第三个里程碑-解决故障

\#\#拷贝 /etc/skel 模板中的内容 到 当前用户家目录

-bash-4.1$ cp /etc/skel/.bash\* ~

-bash-4.1$ ll -a

total 20

drwx------  2 alex888 alex888 4096 Apr  5 10:06 .

drwxr-xr-x. 9 root    root    4096 Apr  5 09:22 ..

-rw-r--r--  1 alex888 alex888   18 Apr  5 10:06 .bash\_logout

-rw-r--r--  1 alex888 alex888  176 Apr  5 10:06 .bash\_profile

-rw-r--r--  1 alex888 alex888  124 Apr  5 10:06 .bashrc

第四个里程碑-检查-重新登录

\[root@oldboyedu35-nb ~\]\# su - alex888

\[alex888@oldboyedu35-nb ~\]$ whoami

alex888

/etc/skel 的企业场景作用：

1、可以把想通知的内容放到skel，让登录的人去看

2、统一初始化新用户的环境变量（所有新用户的模板）

3、面试题，linux命令行出现-bash-4.1$问题原因及解决方法

知识点：export PS1='\[\u@\h \W\t\]$' \#\#临时生效

#### 1.2.5 /etc/default/useradd 文件

useradd

/etc/defalut/useradd 文件时在使用useradd添加用户事放入一个需要调用的一个默认的配置文件，可以使用“useradd -D-\* 参数 ”，这样的命令格式来修改文件里面的内容

#### 1.2.6 /etc/login.defs（了解）

/etc/login.defs文件时用来定义创建用户时需要的一些用户配置信息，如创建用户时，是否需要家目录，家目录权限，UID和GID的范围，用户及密码的有效期限等等

\[oldboy@oldboyedu-35 ~\]$ cat /etc/login.defs

\#

\# Please note that the parameters in this configuration file control the

\# behavior of the tools from the shadow-utils component. None of these

\# tools uses the PAM mechanism, and the utilities that use PAM \(such as the

\# passwd command\) should therefore be configured elsewhere. Refer to

\# /etc/pam.d/system-auth for more information.

\#

\# \*REQUIRED\*

\#   Directory where mailboxes reside, \_or\_ name of file, relative to the

\#   home directory.  If you \_do\_ define both, MAIL\_DIR takes precedence.

\#   QMAIL\_DIR is for Qmail

\#

\#QMAIL\_DIR    Maildir

MAIL\_DIR    /var/spool/mail

\#MAIL\_FILE    .mail

\# Password aging controls:   密码过期时间控制

\#

\#    PASS\_MAX\_DAYS    Maximum number of days a password may be used.

\#    PASS\_MIN\_DAYS    Minimum number of days allowed between password changes.

\#    PASS\_MIN\_LEN    Minimum acceptable password length.

\#    PASS\_WARN\_AGE    Number of days warning given before a password expires.

\#

PASS\_MAX\_DAYS    99999          一个密码最长可以使用的天数：273年

PASS\_MIN\_DAYS    0               更换密码的最小天数

PASS\_MIN\_LEN    5               密码的最小长度

PASS\_WARN\_AGE    7            密码失效前提前多少天数开始警告

\#

\# Min/max values for automatic uid selection in useradd

\#

UID\_MIN              500 最小uid为500，也就是说添加用户时，UID是从500开始的，实际就是这个地方控制的

UID\_MAX            60000 最大UID为60000

\#

\# Min/max values for automatic gid selection in groupadd

\#

GID\_MIN              500    GID 依然是从500开始

GID\_MAX            60000

\#

\# If defined, this command is run when removing a user.

\# It should remove any at/cron/print jobs etc. owned by

\# the user to be removed \(passed as the first argument\).

\#

\#USERDEL\_CMD    /usr/sbin/userdel\_local

\#

\# If useradd should create home directories for users by default

\# On RH systems, we do. This option is overridden with the -m flag on

\# useradd command line.

\#

CREATE\_HOME    yes           是否创用户家目录，默认要求创建，可以用-m参数来控制

\# The permission mask is initialized to this value. If not specified,

\# the permission mask will be initialized to 022.

UMASK           077  创建用户老家/家目录默认的权限

\# This enables userdel to remove user groups if no members exist.

\#

USERGROUPS\_ENAB yes      删除用户同时删除用户组

\# Use SHA512 to encrypt password.

ENCRYPT\_METHOD SHA512

#### 1.2.7 /etc/default/useradd 文件

useradd

/etc/default/useradd 文件是在使用useradd添加用户时的一个需要调用的一个默认的配置文件，可以使用“useradd -D-\* 参数”，这样的命令格式来修改文件里面的内容

\[root@oldboyedu-35 ~\]\# ls -ld /etc/default/useradd

-rw-------. 1 root root 119 Feb  9  2016 /etc/default/useradd

\[root@oldboyedu-35 ~\]\# cat /etc/default/useradd

\# useradd defaults file

GROUP=100

HOME=/home

INACTIVE=-1

EXPIRE=

SHELL=/bin/bash

SKEL=/etc/skel

CREATE\_MAIL\_SPOOL=yes

#### 1.2.8 useradd 添加用户命令

| **useradd参数选项** | **注释说明** |
| :--- | :--- |
| **-c comment** | \#comment===\#注释说明---&gt;新账号password档的说明栏 |
| **-d home\_dir** | \#--&gt;新账号每次登入时所使用的home\_dir。预设值为default\_home内login名称，并当成登入时目录名称 |
| **-e expire\_date** | \#--&gt;※※账号终止日期（账号过期日期）。日期的指定格式为MM-DD-YY或者YYYY-MM-DD |
| **-g initial\_group** | \#--&gt;※※group名称或以数字来做为用户登入起始用户组（group）主要的组。用户组名必须为系统现有存在的名称。用户组数字也须为现有存在的用户组，预设的用户组数字为1 |
| **-G group，\[...\]** | \#---&gt;附加组，定义此用户为多个不同groups的成员。每个用户组使用“，”逗号隔开。用户组名同-g选项的限制。默认值为用户的起始用户组 |
| **-M** | \#--&gt;※※不建议用户家目录，优先于/etc/login.defs文件的设定。一般创建虚拟用户时不建立家目录，部署服务时需要创建虚拟用户 |
| **-s shell** | \#---&gt;※※用户登入后使用的shell名称。默认值为不填写，这样系统会帮你指定预设的登入shell（根据/etc/default/useradd预设的值）cat /etc/shells系统支持的shell |
| **-u uid** | \#--&gt;用户的ID值。这个值必须是唯一的，除非用-o选项，数字不可为负值 |

#### 添加一个虚拟用户mysql

\[root@oldboyedu35-nb ~\]\# \#

\[root@oldboyedu35-nb ~\]\# useradd -s /sbin/nologin -M mysql

\[root@oldboyedu35-nb ~\]\# ll /home/mysql

ls: cannot access /home/mysql: No such file or directory

\[root@oldboyedu35-nb ~\]\# su - mysql

su: warning: cannot change directory to /home/mysql: No such file or directory

This account is currently not available.

### 1.2.9 useradd小结

添加用户alex666，UID指定为999，归属为用户组 root、oldboy、sa成员，并设置其用户注释信息为HandsomeBoy，设置家目录为/alex666，其shell类型为/bin/sh

\[root@oldboyedu35-nb ~\]\# \#添加用户alex666，UID指定为999，归属为用户组 root、oldboy、sa成员，并设置其用户注释信息为HandsomeBoy，设置家目录为/alex666，其shell类型为/bin/sh。

\[root@oldboyedu35-nb ~\]\# groupadd oldboy

groupadd: group 'oldboy' already exists

\[root@oldboyedu35-nb ~\]\# groupadd sa

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# useradd -u 999 -G root,oldboy,sa -c "HandsomeBoy"  -d /alex666 -s /bin/sh alex666

\[root@oldboyedu35-nb ~\]\# id alex666

uid=999\(alex666\) gid=999\(alex666\) groups=999\(alex666\),0\(root\),500\(oldboy\),511\(sa\)

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# grep alex666 /etc/passwd

alex666:x:999:999:HandsomeBoy:/alex666:/bin/sh

\[root@oldboyedu35-nb ~\]\# ll -d /alex666/

drwx------ 2 alex666 alex666 4096 Apr  5 11:39 /alex666/

![](/assets/19-1.jpg)

### 1.2.10 userdel 删除用户相关命令

##### -r 连窝端了

删除用户及用户相关的信息，与这个命令有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

### 1.2.11 usermod用户信息修改相关命令

与usermod有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

![](/assets/tab19-11.png)

必须是唯一的数字（不能为负数）

\[root@oldboyedu-35 ~\]\# grep oldboy /etc/sudoers

%oldboy ALL=\(ALL\)       /bin/touch, /bin/mkdir, /bin/ls

\[root@oldboyedu-35 ~\]\# usermod -G oldboy oldgirl

\[oldgirl@oldboyedu-35 ~\]$ whoami

oldgirl

\[oldgirl@oldboyedu-35 ~\]$ sudo -l

Matching Defaults entries for oldgirl on this host:

!visiblepw, always\\_set\\_home, env\\_reset, env\\_keep="COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR LS\\_COLORS",

env\\_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC\\_ADDRESS LC\\_CTYPE", env\\_keep+="LC\\_COLLATE LC\\_IDENTIFICATION

LC\\_MEASUREMENT LC\\_MESSAGES", env\\_keep+="LC\\_MONETARY LC\\_NAME LC\\_NUMERIC LC\\_PAPER LC\\_TELEPHONE", env\\_keep+="LC\\_TIME

LC\\_ALL LANGUAGE LINGUAS \\_XKB\\_CHARSET XAUTHORITY", secure\\_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User oldgirl may run the following commands on this host:

\\(ALL\\) /bin/touch, \\(ALL\\) /bin/mkdir, \\(ALL\\) /bin/ls

### 1.2.12 groupadd 添加用户组的命令

groupadd    注释说明

-g gid    指定用户组GID值。除非接-o 参数（groupadd -g 1234 -o oldboy），否则ID值必须是唯一的数字（不能为负数）。如果不指定-g参数，则预设值会从500开始

\[root@oldboyedu35-nb ~\]\# groupadd -g 1000 jason007

\[root@oldboyedu35-nb ~\]\# grep jason /etc/group

jason:x:507:

jason888:x:508:

jason007:x:1000:

\[root@oldboyedu35-nb ~\]\# useradd -u 1000 -g jason007 jason007

\[root@oldboyedu35-nb ~\]\# id jason007

uid=1000\(jason007\) gid=1000\(jason007\) groups=1000\(jason007\)

\[root@oldboyedu35-nb ~\]\# useradd -u 2000 oldboy888

\[root@oldboyedu35-nb ~\]\# id oldboy888

uid=2000\(oldboy888\) gid=2000\(oldboy888\) groups=2000\(oldboy888\)

### 1.2.13 企业场景删除用户处理方法

一般不能确认用户相关目录有没有重要数据就不能用-r

删除经验：

1、vi /etc/passwd ,然后注释掉用户，观察1个月，这样出问题可以还原。相当于操作前备份。

2、把登录shell/bin/bash 改成 /sbin/nologin

3、openldap（类似活动目录）账号统一管理的，ldap库里干掉用户。所有服务器全部都没了。

提示：只要删除和修改都要小心谨慎，不需要的请注释

### 1.2.14 内容小结

useradd

/etc/default/useradd 文件作用

/etc/skel目录作用

/etc/login.defs 文件作用

![](/assets/19-2.png)

### 1.2.15 档案

/etc/passwd 使用者账号资讯

/etc/shadow 使用者账号资讯加密

/etc/group 用户组资讯

/etc/gshadow

/etc/default/useradd 定义资讯

/etc/skel 内含定义档的目录

/etc/login.defs 系统广义设定

### 1.2.16 passwd 用户密码相关 修改用户密码

![](/assets/tab19-13.png)

\[root@oldboyedu35-nb ~\]\# echo 123456 \|passwd --stdin oldboy

Changing password for user oldboy.

passwd: all authentication tokens updated successfully.

例子：

\#\#\#添加一个用户 oldboy666  指定他的uid是666  设置密码为123456

\[root@oldboyedu-35 ~\]\# useradd -u 666 oldboy666

\[root@oldboyedu-35 ~\]\# echo 123456\|passwd --stdin oldboy666

Changing password for user oldboy666.

passwd: all authentication tokens updated successfully.

\[root@oldboyedu35-nb ~\]\# useradd -u 666 oldboy666

\[root@oldboyedu35-nb ~\]\# id oldboy666

uid=666\(oldboy666\) gid=666\(oldboy666\) groups=666\(oldboy666\)

\[root@oldboyedu35-nb ~\]\# echo 123456\|passwd --stdin oldboy666

Changing password for user oldboy666.

passwd: all authentication tokens updated successfully.

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ su - oldboy666

Password:

\[oldboy666@oldboyedu35-nb ~\]$ whoami

oldboy666

\[oldboy666@oldboyedu35-nb ~\]$

### 1.2.17 chage 修改用户密码有效期限change age\(密码年纪  密码相关的时间）

![](/assets/tab19-14.png)

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change     : Apr 06, 2017

Password expires     : never

Password inactive     : never

Account expires     : never

Minimum number of days between password change     : 0

Maximum number of days between password change     : 99999

Number of days of warning before password expires    : 7

\[root@oldboyedu35-nb ~\]\# chage -E "2017-04-14" oldboy666

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change     : Apr 06, 2017

Password expires     : Jun 05, 2017

Password inactive     : Jul 05, 2017

Account expires     : Apr 14, 2017

Minimum number of days between password change     : 7

Maximum number of days between password change     : 60

Number of days of warning before password expires    : 10

\[root@oldboyedu35-nb ~\]\# date -s "10 day"

Sun Apr 16 10:06:33 CST 2017

\[root@oldboyedu35-nb ~\]\# chage -E "30 day" oldboy666

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change     : Apr 16, 2017

Password expires     : Jun 15, 2017

Password inactive     : Jul 15, 2017

Account expires     : May 16, 2017

Minimum number of days between password change     : 7

Maximum number of days between password change     : 60

Number of days of warning before password expires    : 10

\[root@oldboyedu35-nb ~\]\# date

Sun Apr 16 10:09:12 CST 2017

\[root@oldboyedu-35 ~\]\# passwd --minimum=7 --maximum=60 --warning=10 --inactive=30 oldboy

Adjusting aging data for user oldboy.

passwd: Success

\[root@oldboyedu-35 ~\]\# chage -l oldboy

Last password change                    : Apr 07, 2017

Password expires                    : Jun 06, 2017

Password inactive                    : Jul 06, 2017

Account expires                        : never

Minimum number of days between password change        : 7

Maximum number of days between password change        : 60

Number of days of warning before password expires    : 10

\[root@oldboyedu-35 ~\]\#

### 1.2.18 企业场景：用户密码管理

1、    密码要复杂8/12位以上字母数字页数字符-keepass（软件，密码存放在本地）lastpass（在线版本）

2、    大的企业用户和密码统一管理（相当于活动目录（AD）,openldap）

3、    动态密码：动态口令，第三方提供自己开发也很简单

4、    /var/log/secure

5、    指纹（find+md5sum+定时任务）

6、    锁头chattr+i +a lsattr

### 1.2.19 示例 下面要求oldboy666用户7天内不能更改密码，60天以后必须修改密码，过期前10天通知oldboy666用户，过期后30天后禁止用户登陆。

\[root@oldboyedu35-nb ~\]\# passwd --minimum=7 --maximum=60 --warning=10 --inactive=30 oldboy666

Adjusting aging data for user oldboy666.

passwd: Success

\[root@oldboyedu35-nb ~\]\# grep oldboy666 /etc/shadow

oldboy666:$6$EkqgoRmJ$dc46Ck1D8Jg22NyrRe4ZagIzcvxLquq4bKWD3eVDVdklO7qFraFsLkUbeJX2o0UeFhu9sdp8f4SLBQ5aG3VF9.:17262:7:60:10:30::

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change : Apr 06, 2017

Password expires : Jun 05, 2017

Password inactive : Jul 05, 2017

Account expires : never

Minimum number of days between password change : 7

Maximum number of days between password change : 60

Number of days of warning before password expires : 10

\[root@oldboyedu35-nb ~\]\# passwd  -n 7 -x 60 -w 10 -i 30 oldboy666

Adjusting aging data for user oldboy666.

passwd: Success

### 1.2.20 用户查询命令小结

需要知道：id w who list lastlog

了解：users groups newgrp

### 1.2.21     查看用户信息

\[root@oldboyedu35-nb ~\]\# id

uid=0\(root\) gid=0\(root\) groups=0\(root\)

\[root@oldboyedu35-nb ~\]\# w

10:31:44 up 1 day, 22:19,  2 users,  load average: 0.00, 0.01, 0.05

USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT

root     pts/0    192.168.56.1     05Apr17  0.00s  1.12s  0.05s w

root     pts/1    192.168.56.1     06Apr17 10days  0.09s  0.09s -bash

\[root@oldboyedu35-nb ~\]\# uptime

10:34:02 up 1 day, 22:22,  2 users,  load average: 0.00, 0.01, 0.05

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# who

root     pts/0        2017-04-05 12:15 \(192.168.56.1\)

root     pts/1        2017-04-06 08:52 \(192.168.56.1\)

\[root@oldboyedu35-nb ~\]\# lastlog

Username         Port     From             Latest

root             pts/1    192.168.56.1     Sun Apr 16 10:37:58 +0800 2017

bin                                        \*\*Never logged in\*\*

daemon                                     \*\*Never logged in\*\*

adm                                        \*\*Never logged in\*\*

lp                                         \*\*Never logged in\*\*

sync                                       \*\*Never logged in\*\*

shutdown                                   \*\*Never logged in\*\*

halt                                       \*\*Never logged in\*\*

mail                                       \*\*Never logged in\*\*

uucp                                       \*\*Never logged in\*\*

operator                                   \*\*Never logged in\*\*

games                                      \*\*Never logged in\*\*

gopher                                     \*\*Never logged in\*\*

ftp                                        \*\*Never logged in\*\*

nobody                                     \*\*Never logged in\*\*

dbus                                       \*\*Never logged in\*\*

vcsa                                       \*\*Never logged in\*\*

abrt                                       \*\*Never logged in\*\*

haldaemon                                  \*\*Never logged in\*\*

ntp                                        \*\*Never logged in\*\*

saslauth                                   \*\*Never logged in\*\*

postfix                                    \*\*Never logged in\*\*

sshd                                       \*\*Never logged in\*\*

tcpdump                                    \*\*Never logged in\*\*

oldboy                                     \*\*Never logged in\*\*

junge                                      \*\*Never logged in\*\*

alex                                       \*\*Never logged in\*\*

oldgirl                                    \*\*Never logged in\*\*

test                                       \*\*Never logged in\*\*

kevin                                      \*\*Never logged in\*\*

jason                                      \*\*Never logged in\*\*

jason888                                   \*\*Never logged in\*\*

mysql                                      \*\*Never logged in\*\*

alex666                                    \*\*Never logged in\*\*

jason007                                   \*\*Never logged in\*\*

oldboy888                                  \*\*Never logged in\*\*

oldboy666                                  \*\*Never logged in\*\*

\[root@oldboyedu35-nb ~\]\# \#\#\#\#登录----本地登录（输入用户名密码）或者远程登录  （xshell crt putty\)

## 1.3 linux用户身份切换命令

在linux系统中，每个文件、目录和进程，都是归属于某一个用户的，没有其他用户的许可，其他的普通用户是无法操作的，除外。root用户的特权还表现在root可以超越任何用户和用户组来对文件或目录进行读取、修改或删除（在系统正常的许可范围内）；对可执行程序的执行，终止；对硬件设备的添加、创建和移除等；也可以对文件和目录进行属主和权限进行修改。

### 1.3.1 su 命令

su \[选项参数\] \[用户\]

![](/assets/tab19-15.png)

### 1.3.2 su 命令的总结

1）普通用户切换到root用户，可使用su -或su - root.必须输入root的密码才能完成切换。

2）root用户切换到普通用户，可使用“su - 普通用户”的写法。不需要输入任何密码就能完成切换。切换到普通用户后，在执行一些命令如ifconfig时，可能会遇到环境变量PATH路径问题而找不到某些系统命令（一般/sbin,/usr/sbin等下面的命令），这时就需要将普通用户的PATH，配置成root的PATH内容，前面的文章已讲解过这个配置方法，不清楚的同学，可以查询一下。提示：Centos6.4以上系统不存在这个问题

3）如果仅希望以某用户的角色执行命令，而不直接切换到该用户下操作，可以使用su - 用户名 -c “命令”的方式.

su 和su - 的区别 谈学习linux运维方法

oldboy.blog.51cto.com/2561410/1053606

### 1.3.3 su 命令的优缺点

毫无疑问，切换用户身份的su命令为我们管理linux系统带来了很多方便，通过切换到root下，可以完成各种系统管理工作，只要任何一个普通用户知道了root用户的密码，都可以以普通用户的身份切换到root来完成本来无法完成的系统管理工作。

但是，这样通过su命令切换到root后，也带来了很大安全管理问题，比如系统有8个普通用户，都可以通过切换到root身份进行系统管理，甚至还可以改掉root的密码，让其他的普通用户无法再实现系统管理，还有，这么多用户中，有任何一人对系统操作的重大失误，都可以导致整个系统崩溃或数据损失。这样的非集权式管理，在一定程序上就对系统的安全造成了较大威胁。在工作中，几乎有一半的问题来自于内部。

所以使用su命令切换身份在多个系统管理员共同管理的场合，并不是最好的选择，因此，我建议如果是一般的中小公司不超过3个管理员时，为了管理方便，使用su来共同管理是可以接受的。

我们既希望超级用户root密码掌握在少数或唯一的管理员手中，又希望多个系统管理员能够完成更多更复杂的系统管理工作。那么，如何解决多个系统管理员都能管理系统而又不让超级权限泛滥的需求呢？这就需要sudo命令来替代或结合su命令来完成这样的苛刻且必要的管理需求。

优点：

1，必须知道root用户的密码

2，我们希望普通用户可以临时做回皇帝，但是我们不想给root用户的密码，--sudo解决

3，大部分企业故障，在工作中几乎有一半的问题来自于内部。

4，安全，最小化

### 1.3.4 课后作业：linux root用户密码忘记了，如何找回来？

进入单用户，把/etc/passwd 删除清空，然后在进入命令行模式

### 1.3.5 实例：

\[root@oldboyedu35-nb ~\]\# usermod -L oldboy666

\[root@oldboyedu35-nb ~\]\# su - oldboy666

\[oldboy666@oldboyedu35-nb ~\]$ logout

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ su - oldboy666

Password:

su: incorrect password

\[oldboy@oldboyedu35-nb ~\]$ su - oldboy666

Password:

su: incorrect password

\[oldboy@oldboyedu35-nb ~\]$ logout

\[root@oldboyedu35-nb ~\]\# usermod -U oldboy666

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ su - oldboy666

Password:

\[oldboy666@oldboyedu35-nb ~\]$ logout

\[oldboy@oldboyedu35-nb ~\]$ logout

\[root@oldboyedu35-nb ~\]\# \#\#\#如果一个用户被锁定了，不要用root给它修改密码

\[root@oldboyedu35-nb ~\]\# \#\#\#修改密码之后锁头自动打开

\[root@oldboyedu35-nb ~\]\# echo $PATH

/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

\[root@oldboyedu35-nb ~\]\# su oldboy

\[oldboy@oldboyedu35-nb root\]$ echo $PATH

/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

\[oldboy@oldboyedu35-nb root\]$ pwd

/root

\[oldboy@oldboyedu35-nb root\]$ ls

ls: cannot open directory .: Permission denied

\[oldboy@oldboyedu35-nb root\]$ ll

ls: cannot open directory .: Permission denied

\[oldboy@oldboyedu35-nb root\]$ cd

\[oldboy@oldboyedu35-nb ~\]$ exit

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ echo $PATH

/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/oldboy/bin

\[root@oldboyedu35-nb ~\]\# \#我想临时切换到oldboy用户下面 执行命令whoami

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ whoami

oldboy

\[oldboy@oldboyedu35-nb ~\]$ logout

\[root@oldboyedu35-nb ~\]\# su - oldboy -c  whoami

oldboy

\[root@oldboyedu35-nb ~\]\# su - oldboy --session-command='echo $PATH'

/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/oldboy/bin

### 1.3.6 sudo的执行过程

![](/assets/tab19-20.png)

### 1.3.7 sudo 命令

sudo \[参数选项\] 命令

![](/assets/tab19-16.png)

### 1.3.8 更改授权/etc/sudoers 文件的几个方法

1）    方法一：执行visudo 命令自动编辑/etc/sudoers 文件（推荐）

root  ALL=\(ALL\)  ALL

oldboy ALL=\(ALL\)  ALL

\#---&gt;前面sudo实例2的权限，同样可以这样设置。当然，位置未必非要在原有的配置文件root权限的先

特别说明：在没有特殊的需要的前提下，请大家一定要使用这个方法，这也是老南京建议读者使用的方法，这个方法是最安全的授权方法，缺点就是必须和系统交互才能完成授权

检查

\[root@oldboyedu-35 ~\]\# ll /etc/sudoers

-r--r-----. 1 root root 4941 Apr  7 23:27 /etc/sudoers

\[root@oldboyedu-35 ~\]\# visudo -c

/etc/sudoers: parsed OK

2\)使用echo &gt;&gt;/etc/sudoers 直接追加

3\)使用用户组的方式实现sudo授权

%sa         ALL=\(ALL\)             ALL

\#--&gt; 注意用户组授权普通用户的区别，开头为“%”百分号。sa组同用户一样必须是已经存在的，是系统的用户组

### 1.3.9 /etc/sudoers 的规则大致可分为两类

一类是别名定义

另一类是授权规则

别名定义并不是必须的，只是在授权规则多的时候更方便授权，但授权规则是必须的、

别名类型（Alias\_Type）:别名类型包括如下四种：

1、Host\_Alias 定义主机别名

2、User\_Alias 用户别名

3、Runas\_Alias Runas别名

4、Cmnd\_Alias 命令别名

### 1.3.10 回顾下别名和具体授权配置的关系，sudo授权

![](/assets/tab19-17.png)

### 1.3.11 sudo 小结

### 但以上直接修改sudoers的配置文件方法有以下需要注意的几点：

1. 如何修改sudoers

visudo

echo命令是追加“&gt;&gt;”,不是重定向“&gt;”，除了echo外，可以用cat，sed等命令实现类似的功能。

修改操作完成一定要执行visudo -c进行语法检查，这弥补了直接修改没有语法检查的不足。

2.权限：确保/etc/sudoers权限是正确的（-r--r----）,权限不对会导致sudo功能异常（Centos6权限不对也可以登录，但是/etc/sudoers是440是最安全的）

3.权限：及时对授权的操作进行测试，验证是否正确（最好不要退出当权授权窗口，以便发现问题及时恢复）。

4.留后路：确保知道正确的root用户密码，以便在sudo出现问题时可以通过普通用户等执行su - 命令切换到root进行恢复

看到了吧，有这么多需要注意的问题，如果不注意，很可能会带来灾难性后果（聘请老男孩做技术顾问

的一个公司的下属曾经就因为不按规范修改sudoer文件，导致所以普通用户无法执行sudo权限，而又恰

巧忘记了root密码（平时不需要root密码管理了），因此只能跑机房通过破解root密码登陆来恢复sudoer

文件配置，影响业务不说，这个遭罪啊！），因此，没有特殊紧急批量增加sudoers文件内容的时候，建

议通过visudo来编辑修改，毕竟系统安全是相当重要的

### 1.3.12 实例（尚方宝剑）

\[root@oldboyedu35-nb ~\]\# \#\#\#给 oldboy  尚方宝剑   useradd

\[root@oldboyedu35-nb ~\]\# \#1.编辑配置文件

\[root@oldboyedu35-nb ~\]\# \#crontab -e   ------ visudo

\[root@oldboyedu35-nb ~\]\# visudo

### 91行后面添加

### oldboy  ALL=\(ALL\)       /usr/sbin/useradd

\[root@oldboyedu35-nb ~\]\# \#2.查看

\[root@oldboyedu35-nb ~\]\# grep oldboy /etc/sudoers

oldboy    ALL=\(ALL\)     /usr/sbin/useradd

\[root@oldboyedu35-nb ~\]\# \#3.测试

\[root@oldboyedu35-nb ~\]\# su - oldboy

\[oldboy@oldboyedu35-nb ~\]$ useradd alex999

-bash: /usr/sbin/useradd: Permission denied

\[oldboy@oldboyedu35-nb ~\]$

\[oldboy@oldboyedu35-nb ~\]$ \#4.查看一下当前用户有什么尚方宝剑

\[oldboy@oldboyedu35-nb ~\]$ sudo -l

We trust you have received the usual lecture from the local System

Administrator. It usually boils down to these three things:

\\#1\\) Respect the privacy of others.

\\#2\\) Think before you type.

\\#3\\) With great power comes great responsibility.

\[sudo\] password for oldboy:

Matching Defaults entries for oldboy on this host:

!visiblepw, always\\_set\\_home, env\\_reset, env\\_keep="COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR LS\\_COLORS",

env\\_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC\\_ADDRESS LC\\_CTYPE", env\\_keep+="LC\\_COLLATE LC\\_IDENTIFICATION

LC\\_MEASUREMENT LC\\_MESSAGES", env\\_keep+="LC\\_MONETARY LC\\_NAME LC\\_NUMERIC LC\\_PAPER LC\\_TELEPHONE", env\\_keep+="LC\\_TIME

LC\\_ALL LANGUAGE LINGUAS \\_XKB\\_CHARSET XAUTHORITY", secure\\_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User oldboy may run the following commands on this host:

\\(ALL\\) /usr/sbin/useradd

\[oldboy@oldboyedu35-nb ~\]$ sudo useradd alex12306

\[oldboy@oldboyedu35-nb ~\]$ id alex12306

uid=2001\(alex12306\) gid=2001\(alex12306\) groups=2001\(alex12306\)

\[oldboy@oldboyedu35-nb ~\]$ sudo -l

Matching Defaults entries for oldboy on this host:

!visiblepw, always\\_set\\_home, env\\_reset, env\\_keep="COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR LS\\_COLORS",

env\\_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC\\_ADDRESS LC\\_CTYPE", env\\_keep+="LC\\_COLLATE LC\\_IDENTIFICATION

LC\\_MEASUREMENT LC\\_MESSAGES", env\\_keep+="LC\\_MONETARY LC\\_NAME LC\\_NUMERIC LC\\_PAPER LC\\_TELEPHONE", env\\_keep+="LC\\_TIME

LC\\_ALL LANGUAGE LINGUAS \\_XKB\\_CHARSET XAUTHORITY", secure\\_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User oldboy may run the following commands on this host:

```
\(ALL\) /usr/sbin/useradd
```

\[oldboy@oldboyedu35-nb ~\]$ sudo rm -f /root/\*

Sorry, user oldboy is not allowed to execute '/bin/rm -f /root/\*' as root on oldboyedu35-nb.

\[oldboy@oldboyedu35-nb ~\]$ \#\#抱歉，用户oldboy不能以root用户的身份执行 rm命令

### 1.3.13 案例  如何快速的查找某个目录下存在着大量的inode

1.目录的大小比较大

2.目录下面的文件比较多

find /oldboy

/oldboy/1

/oldboy/2

/oldboy/3

/oldboy/4

/oldboy/5

/oldboy/6

/oldboy/7

/oldboy/8

/oldboy/9

/oldboy/10

oldboy目录出现的次数  ?????    目录下面的文件数量

### 1.3.14 回顾下别名和具体授权配置的关系

![](/assets/tab19-18.png)

### 1.3.15 工作中一个软件tomcat,以oldboy的身份运行中

重启服务器的时候，我想让tomcat继续以oldboy的身份运行。

让一个软件开机自启动

1\)chkconfig

2\)/etc/rc.local

让tomcat开机启动的时候 以oldboy的身份运行

su - oldboy -c 启动tomcat

放在 /etc/rc.local

su - oldboy -c 启动tomcat

\[tddoc@td-2-1 ~\]$ ps -ef\|grep tddoc  \#→查看包含tddoc用户的服务进程。

tddoc    9042     1  0 Jan16 ?        00:00:02 java -server -Xmn125M -Xms512M -Xmx512M -Xss2048k -Djava.rmi.server.logCalls=false -Dsun.rmi.transport.tcp.logLevel=WARNING -Xloggc:/home/tddoc/run/resin/logs/gc.log -jar /home/tddoc/run/resin/lib/resin.jar -server a

\#→提示：这是一个resin（提供java服务的软件）的服务进程，当前服务用户是tddoc。

这个时候我们就面临一个问题，如何让系统在每一次开机时也要自动以普通用户启动指定的服务脚本呢？答案在下面：

\[root@tdi-2-1 ~\]\# tail -5 /etc/rc.local \#→把要执行的脚本放入开机自启动配置文件/etc/rc.local中。

\#\#\#\#\#\#\#\#分用户方案启动服务命令\#\#\#\#\#\#\#\#

su - tddoc  -c '/bin/sh /home/tddoc/bin/deploy.sh'

### 1.3.16 别名的修改例子

例子：

创建一个用户别名ADMINS = oldboy,oldgirl,alex

创建命令别名

授权NETWORKING,SERIVCES命令

Cmnd\_Alias NETWORKING = /sbin/route, /sbin/ifconfig, /bin/ping

Cmnd\_Alias SERVICES = /sbin/service, /sbin/chkconfig

放在/etc/sudoers（visudo\) 最后一行

su - alex

sudo -l

\#\#\#第一个里程碑-添加用户并统一密码

useradd oldboy

useradd oldgirl

useradd alex

echo 123456 \|passwd --stdin oldboy

echo 123456 \|passwd --stdin oldgirl

echo 123456 \|passwd --stdin alex

\#\#\#第二个里程碑-修改配置文件

\#1.创建用户别名

User\_Alias ADMINS = oldboy, oldgirl, alex

\#2.创建命令别名

Cmnd\_Alias NETWORKING = /sbin/route, /sbin/ifconfig, /bin/ping

Cmnd\_Alias SERVICES = /sbin/service, /sbin/chkconfig

\#3.授予尚方宝剑 黄马褂

\#root ALL=\(ALL\)  ALL

ADMINS  ALL=\(ALL\) NETWORKING, SERVICES

\#4.\*\*\*\*\*\*把原来 oldboy  oldgirl 授权 注释

配置文件的内容：

User\_Alias ADMINS = oldboy, oldgirl, alex

Cmnd\_Alias NETWORKING = /sbin/route, /sbin/ifconfig, /bin/ping

Cmnd\_Alias SERVICES = /sbin/service, /sbin/chkconfig

ADMINS  ALL=\(ALL\) NETWORKING, SERVICES

\#\#\#第三个里程碑-测试检查

su - alex

sudo -l

oldboy            ALL=\(ALL\)                                                       ALL

用户（用户别名）  可以在哪一台机器上面执行sudo=\(你可以以谁的身份执行sudo命令\)   命令（命令别名）

### 1.3.17 总结

1、和用户相关的配置文件知识点：

/etc/passwd 账号文件及不同列内容

/etc/shadow 账号密码文件及不同列内容

/etc/group   组的文件及不同列内容

/etc/gshadow组密码文件及不同列内容

2、用户管理命令

useradd -u -g -G -s -M -e -c -d

初始化用户对应的几个文件/etc/skel,/etc/default/useradd,/etc/login.defs

userdel -r

usermod -u -g -G -s -M -e -c -d -L -U -l

chage -l（小写字母l） -E -M -W -m -I\(大写字母i\)

passwd --stdin -n -i -w -x  \(suid位重点\)   =====&gt;setuid passwd  setgid locate   粘滞位 /tmp

su

sudo

visudo

3、组管理命令

groupadd -g

groupdel

groupmod

id w last

## 1.4 sudo日志审计

![](/assets/19-5.png)

echo "Defaults        logfile=/var/log/sudo.log"&gt;&gt;/etc/sudoers

visudo -c

测试：root用户下

\[root@oldboyedu-35 tmp\]\# tailf /var/log/sudo.log

Apr  7 23:54:10 : oldboy : TTY=pts/1 ; PWD=/home/oldboy ; USER=root ;

COMMAND=list

Apr  8 00:24:36 : oldboy : command not allowed ; TTY=pts/1 ; PWD=/home/oldboy ;

USER=root ; COMMAND=/usr/bin/passwd root

测试：oldboy用户下

\[oldboy@oldboyedu-35 ~\]$ sudo passwd root

\[sudo\] password for oldboy:

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd root' as root on oldboyedu-35.

### 1.4.1 sudo授权最小化 例题：给oldboy用户授权passwd命令，安全不能把皇帝推翻

第一个里程碑-不让修改root密码

oldboy  ALL=\(ALL\)       /usr/bin/passwd, ! /usr/bin/passwd root

oldboy用户:sudo passwd root   XXXXX

oldboy：   sudo passwd        如何限制？

解决方法：用户修改密码的时候 必须加上用户名

第二个里程碑-不让修改root  sudo passwd

\#\#限制的方法 --用户修改密码的时候 必须加上用户名

oldboy  ALL=\(ALL\)       /usr/bin/passwd \[a-zA-Z0-9\]\*

第三个里程碑-彻底不让修改root密码

oldboy  ALL=\(ALL\)       /usr/bin/passwd \[a-zA-Z0-9\]\*, ! /usr/bin/passwd root

\[oldboy@oldboyedu-35 ~\]$ sudo passwd

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd' as root on oldboyedu-35.

\[oldboy@oldboyedu-35 ~\]$ sudo passwd root

Sorry, user oldboy is not allowed to execute '/usr/bin/passwd root' as root on oldboyedu-35.

### 1.4.2 .sudo权限集中管理项目

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

Cmnd\_Alias   USERCMD = /usr/sbin/useradd, /usr/sbin/userdel, /usr/bin/passwd , /bin/chown, /bin/chmod

Cmnd\_Alias   DISKCMD = /sbin/fdisk, /sbin/parted

Cmnd\_Alias   NETMAGCMD = /sbin/ifconfig, /etc/init.d/network

Cmnd\_Alias   CTRLCMD = /usr/sbin/reboot, /usr/sbin/halt

Cmnd\_Alias   LOOKCMD = /bin/grep, /usr/bin/tail, /bin/cat, /usr/bin/less

\#\#\#\#\#第三个里程碑---演戏---规划每个演员做什么动作 （每个用户执行什么命令）

开发人员：  User\_Alias KAIFA\_ADMINS = kaifa01, kaifa02

```
        命令权限：LOOKCMD

        身份权限：root
```

运维人员：  User\_Alias OLD\_ADMINS = oldboy, oldgirl, %sa

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

\#root    ALL=\(ALL\)       ALL

\#用户     机器 角色       命令

KAIFA\_ADMINS ALL=\(root\)    LOOKCMD

ADMINS       ALL=\(root\)    USERCMD, DISKCMD, NETMAGCMD, CTRLCMD, LOOKCMD

NETADMINS    ALL=\(root\)    NETMAGCMD

\#\#\#\#第五个里程碑-后期5毛钱特效--修改配置文件

\#\#\#快速命令

\#\#\#useradd

groupadd sa

useradd leo     && echo 123\|passwd --stdin leo

useradd maya    && echo 123\|passwd --stdin maya

useradd zuma    && echo 123\|passwd --stdin zuma

useradd ett     && echo 123\|passwd --stdin ett

useradd kaifa01 && echo 123\|passwd --stdin kaifa01

useradd kaifa02 && echo 123\|passwd --stdin kaifa02

\#\#\#user alias

User\_Alias KAIFA\_ADMINS = kaifa01, kaifa02

User\_Alias ADMINS = oldboy, oldgirl, %sa

User\_Alias NETADMINS = leo,maya

\#\#command alias

Cmnd\_Alias   USERCMD = /usr/sbin/useradd, /usr/sbin/userdel, \

/usr/bin/passwd \[A-Za-z\]\*, /bin/chown, /bin/chmod

Cmnd\_Alias   DISKCMD = /sbin/fdisk, /sbin/parted

Cmnd\_Alias   NETMAGCMD = /sbin/ifconfig, /etc/init.d/network

Cmnd\_Alias   CTRLCMD = /usr/sbin/reboot, /usr/sbin/halt

Cmnd\_Alias   LOOKCMD = /bin/grep, /usr/bin/tail, /bin/cat, /usr/bin/less

\#\#rules

KAIFA\_ADMINS ALL=\(root\)    LOOKCMD

ADMINS   ALL=\(root\)    USERCMD, DISKCMD, NETMAGCMD, CTRLCMD, LOOKCMD

NETADMINS ALL=\(root\)   NETMAGCMD

\#\#\#\#第六个里程碑-试映---检查

1. 多开几个窗口--标记好了

2. 大象放冰箱-一步一步来

### 1.4.3 sudo 配置文件/etc/sudoers 授权规则注意事项总结：

1）    授权规则中的所有ALL字符串必须为大写字母

2）    允许执行的命令是有顺序的。前面的为允许，后面的为禁止，执行命令的顺序是从后往前执行的

/usr/sbin/\*，/sbin/\*，！/usr/sbin/visudo,!/sbin/fdisk

再次强调，禁止的命令尽量放在后面

3）    一行内容超长可以用“\”反斜线换行

4）    ！叹号表示非，就是命令取反的意思，即禁止执行的命令

5）    根据实际情况，来分类制作命令别名，用什么就给什么权限

