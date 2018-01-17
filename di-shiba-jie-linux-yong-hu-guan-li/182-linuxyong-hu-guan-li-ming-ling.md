#### 管理用户命令汇总 {#121-管理用户命令汇总}

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

#### 1.2.2 管理用户组命令汇总 {#122-管理用户组命令汇总}

| 命令 | 注释说明 |
| :--- | :--- |
| groupadd | \#--&gt;※添加用户组 |
| groupdel | 删除用户组 |
| groupmod | 修改用户组信息 |
| gpasswd | 为用户组设置密码 |
| groups | 显示用户所属的用户组 |
| newgrp | 更改用户所属的有效用户组 |

#### 1.2.3 /etc/skel目录 {#123-etcskel目录}

新用户的老家的默认的样子，从/etc/skel目录复制过来

/etc/skel 目录是用来存放新用户环境变量文件的目录，当我们添加新用户时，这个目录下的所有文件会自动被复制到新添加的用户的家目录下

默认情况下，/etc/skel 目录下的所有文件都是隐藏文件（以点开头的文件）;通过修改、添加、删除/etc/skel目录下的文件，我们可为新创建的用户提供统一的、标准的、初始化用户环境（给所有新用户的一个家默认样子）

#### 1.2.4 企业面试案例】：请问如下登录环境故障的原理及解决办法？ {#124-企业面试案例】：请问如下登录环境故障的原理及解决办法？}

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

drwx------ 2 alex888 alex888 4096 Apr 5 10:06 .

drwxr-xr-x. 9 root root 4096 Apr 5 09:22 ..

-rw-r--r-- 1 alex888 alex888 18 Apr 5 10:06 .bash\_logout

-rw-r--r-- 1 alex888 alex888 176 Apr 5 10:06 .bash\_profile

-rw-r--r-- 1 alex888 alex888 124 Apr 5 10:06 .bashrc

第四个里程碑-检查-重新登录

\[root@oldboyedu35-nb ~\]\# su - alex888

\[alex888@oldboyedu35-nb ~\]$ whoami

alex888

/etc/skel 的企业场景作用：

1、可以把想通知的内容放到skel，让登录的人去看

2、统一初始化新用户的环境变量（所有新用户的模板）

3、面试题，linux命令行出现-bash-4.1$问题原因及解决方法

知识点：export PS1='\[\u@\h \W\t\]$' \#\#临时生效

#### 1.2.5 /etc/default/useradd 文件 {#125-etcdefaultuseradd-文件}

useradd

/etc/defalut/useradd 文件时在使用useradd添加用户事放入一个需要调用的一个默认的配置文件，可以使用“useradd -D-\* 参数 ”，这样的命令格式来修改文件里面的内容

#### 1.2.6 /etc/login.defs（了解） {#126-etclogindefs（了解）}

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

\# Directory where mailboxes reside, \_or\_ name of file, relative to the

\# home directory. If you \_do\_ define both, MAIL\_DIR takes precedence.

\# QMAIL\_DIR is for Qmail

\#

\#QMAIL\_DIR Maildir

MAIL\_DIR /var/spool/mail

\#MAIL\_FILE .mail

\# Password aging controls: 密码过期时间控制

\#

\# PASS\_MAX\_DAYS Maximum number of days a password may be used.

\# PASS\_MIN\_DAYS Minimum number of days allowed between password changes.

\# PASS\_MIN\_LEN Minimum acceptable password length.

\# PASS\_WARN\_AGE Number of days warning given before a password expires.

\#

PASS\_MAX\_DAYS 99999 一个密码最长可以使用的天数：273年

PASS\_MIN\_DAYS 0 更换密码的最小天数

PASS\_MIN\_LEN 5 密码的最小长度

PASS\_WARN\_AGE 7 密码失效前提前多少天数开始警告

\#

\# Min/max values for automatic uid selection in useradd

\#

UID\_MIN 500 最小uid为500，也就是说添加用户时，UID是从500开始的，实际就是这个地方控制的

UID\_MAX 60000 最大UID为60000

\#

\# Min/max values for automatic gid selection in groupadd

\#

GID\_MIN 500 GID 依然是从500开始

GID\_MAX 60000

\#

\# If defined, this command is run when removing a user.

\# It should remove any at/cron/print jobs etc. owned by

\# the user to be removed \(passed as the first argument\).

\#

\#USERDEL\_CMD /usr/sbin/userdel\_local

\#

\# If useradd should create home directories for users by default

\# On RH systems, we do. This option is overridden with the -m flag on

\# useradd command line.

\#

CREATE\_HOME yes 是否创用户家目录，默认要求创建，可以用-m参数来控制

\# The permission mask is initialized to this value. If not specified,

\# the permission mask will be initialized to 022.

UMASK 077 创建用户老家/家目录默认的权限

\# This enables userdel to remove user groups if no members exist.

\#

USERGROUPS\_ENAB yes 删除用户同时删除用户组

\# Use SHA512 to encrypt password.

ENCRYPT\_METHOD SHA512

#### 1.2.7 /etc/default/useradd 文件 {#127-etcdefaultuseradd-文件}

useradd

/etc/default/useradd 文件是在使用useradd添加用户时的一个需要调用的一个默认的配置文件，可以使用“useradd -D-\* 参数”，这样的命令格式来修改文件里面的内容

\[root@oldboyedu-35 ~\]\# ls -ld /etc/default/useradd

-rw-------. 1 root root 119 Feb 9 2016 /etc/default/useradd

\[root@oldboyedu-35 ~\]\# cat /etc/default/useradd

\# useradd defaults file

GROUP=100

HOME=/home

INACTIVE=-1

EXPIRE=

SHELL=/bin/bash

SKEL=/etc/skel

CREATE\_MAIL\_SPOOL=yes

#### 1.2.8 useradd 添加用户命令 {#128-useradd-添加用户命令}

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

#### 添加一个虚拟用户mysql {#添加一个虚拟用户mysql}

\[root@oldboyedu35-nb ~\]\# \#

\[root@oldboyedu35-nb ~\]\# useradd -s /sbin/nologin -M mysql

\[root@oldboyedu35-nb ~\]\# ll /home/mysql

ls: cannot access /home/mysql: No such file or directory

\[root@oldboyedu35-nb ~\]\# su - mysql

su: warning: cannot change directory to /home/mysql: No such file or directory

This account is currently not available.

### 1.2.9 useradd小结 {#129-useradd小结}

添加用户alex666，UID指定为999，归属为用户组 root、oldboy、sa成员，并设置其用户注释信息为HandsomeBoy，设置家目录为/alex666，其shell类型为/bin/sh

\[root@oldboyedu35-nb ~\]\# \#添加用户alex666，UID指定为999，归属为用户组 root、oldboy、sa成员，并设置其用户注释信息为HandsomeBoy，设置家目录为/alex666，其shell类型为/bin/sh。

\[root@oldboyedu35-nb ~\]\# groupadd oldboy

groupadd: group 'oldboy' already exists

\[root@oldboyedu35-nb ~\]\# groupadd sa

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# useradd -u 999 -G root,oldboy,sa -c "HandsomeBoy" -d /alex666 -s /bin/sh alex666

\[root@oldboyedu35-nb ~\]\# id alex666

uid=999\(alex666\) gid=999\(alex666\) groups=999\(alex666\),0\(root\),500\(oldboy\),511\(sa\)

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# grep alex666 /etc/passwd

alex666:x:999:999:HandsomeBoy:/alex666:/bin/sh

\[root@oldboyedu35-nb ~\]\# ll -d /alex666/

drwx------ 2 alex666 alex666 4096 Apr 5 11:39 /alex666/

![](https://www.luffycity.com/linux-book/assets/19-1.jpg)

### 1.2.10 userdel 删除用户相关命令 {#1210-userdel-删除用户相关命令}

##### -r 连窝端了 {#r-连窝端了}

删除用户及用户相关的信息，与这个命令有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

### 1.2.11 usermod用户信息修改相关命令 {#1211-usermod用户信息修改相关命令}

与usermod有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

![](https://www.luffycity.com/linux-book/assets/tab19-11.png)

必须是唯一的数字（不能为负数）

\[root@oldboyedu-35 ~\]\# grep oldboy /etc/sudoers

%oldboy ALL=\(ALL\) /bin/touch, /bin/mkdir, /bin/ls

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

### 1.2.12 groupadd 添加用户组的命令 {#1212-groupadd-添加用户组的命令}

groupadd 注释说明

-g gid 指定用户组GID值。除非接-o 参数（groupadd -g 1234 -o oldboy），否则ID值必须是唯一的数字（不能为负数）。如果不指定-g参数，则预设值会从500开始

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

### 1.2.13 企业场景删除用户处理方法 {#1213-企业场景删除用户处理方法}

一般不能确认用户相关目录有没有重要数据就不能用-r

删除经验：

1、vi /etc/passwd ,然后注释掉用户，观察1个月，这样出问题可以还原。相当于操作前备份。

2、把登录shell/bin/bash 改成 /sbin/nologin

3、openldap（类似活动目录）账号统一管理的，ldap库里干掉用户。所有服务器全部都没了。

提示：只要删除和修改都要小心谨慎，不需要的请注释

### 1.2.14 内容小结 {#1214-内容小结}

useradd

/etc/default/useradd 文件作用

/etc/skel目录作用

/etc/login.defs 文件作用

![](https://www.luffycity.com/linux-book/assets/19-2.png)

### 1.2.15 档案 {#1215-档案}

/etc/passwd 使用者账号资讯

/etc/shadow 使用者账号资讯加密

/etc/group 用户组资讯

/etc/gshadow

/etc/default/useradd 定义资讯

/etc/skel 内含定义档的目录

/etc/login.defs 系统广义设定

### 1.2.16 passwd 用户密码相关 修改用户密码 {#1216-passwd-用户密码相关-修改用户密码}

![](https://www.luffycity.com/linux-book/assets/tab19-13.png)

\[root@oldboyedu35-nb ~\]\# echo 123456 \|passwd --stdin oldboy

Changing password for user oldboy.

passwd: all authentication tokens updated successfully.

例子：

\#\#\#添加一个用户 oldboy666 指定他的uid是666 设置密码为123456

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

### 1.2.17 chage 修改用户密码有效期限change age\(密码年纪 密码相关的时间） {#1217-chage-修改用户密码有效期限change-age密码年纪--密码相关的时间）}

![](https://www.luffycity.com/linux-book/assets/tab19-14.png)

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change : Apr 06, 2017

Password expires : never

Password inactive : never

Account expires : never

Minimum number of days between password change : 0

Maximum number of days between password change : 99999

Number of days of warning before password expires : 7

\[root@oldboyedu35-nb ~\]\# chage -E "2017-04-14" oldboy666

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change : Apr 06, 2017

Password expires : Jun 05, 2017

Password inactive : Jul 05, 2017

Account expires : Apr 14, 2017

Minimum number of days between password change : 7

Maximum number of days between password change : 60

Number of days of warning before password expires : 10

\[root@oldboyedu35-nb ~\]\# date -s "10 day"

Sun Apr 16 10:06:33 CST 2017

\[root@oldboyedu35-nb ~\]\# chage -E "30 day" oldboy666

\[root@oldboyedu35-nb ~\]\# chage -l oldboy666

Last password change : Apr 16, 2017

Password expires : Jun 15, 2017

Password inactive : Jul 15, 2017

Account expires : May 16, 2017

Minimum number of days between password change : 7

Maximum number of days between password change : 60

Number of days of warning before password expires : 10

\[root@oldboyedu35-nb ~\]\# date

Sun Apr 16 10:09:12 CST 2017

\[root@oldboyedu-35 ~\]\# passwd --minimum=7 --maximum=60 --warning=10 --inactive=30 oldboy

Adjusting aging data for user oldboy.

passwd: Success

\[root@oldboyedu-35 ~\]\# chage -l oldboy

Last password change : Apr 07, 2017

Password expires : Jun 06, 2017

Password inactive : Jul 06, 2017

Account expires : never

Minimum number of days between password change : 7

Maximum number of days between password change : 60

Number of days of warning before password expires : 10

\[root@oldboyedu-35 ~\]\#

### 1.2.18 企业场景：用户密码管理 {#1218-企业场景：用户密码管理}

1、 密码要复杂8/12位以上字母数字页数字符-keepass（软件，密码存放在本地）lastpass（在线版本）

2、 大的企业用户和密码统一管理（相当于活动目录（AD）,openldap）

3、 动态密码：动态口令，第三方提供自己开发也很简单

4、 /var/log/secure

5、 指纹（find+md5sum+定时任务）

6、 锁头chattr+i +a lsattr

### 1.2.19 示例 下面要求oldboy666用户7天内不能更改密码，60天以后必须修改密码，过期前10天通知oldboy666用户，过期后30天后禁止用户登陆。 {#1219-示例-下面要求oldboy666用户7天内不能更改密码，60天以后必须修改密码，过期前10天通知oldboy666用户，过期后30天后禁止用户登陆。}

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

\[root@oldboyedu35-nb ~\]\# passwd -n 7 -x 60 -w 10 -i 30 oldboy666

Adjusting aging data for user oldboy666.

passwd: Success

### 1.2.20 用户查询命令小结 {#1220-用户查询命令小结}

需要知道：id w who list lastlog

了解：users groups newgrp

### 1.2.21 查看用户信息 {#1221-----查看用户信息}

\[root@oldboyedu35-nb ~\]\# id

uid=0\(root\) gid=0\(root\) groups=0\(root\)

\[root@oldboyedu35-nb ~\]\# w

10:31:44 up 1 day, 22:19, 2 users, load average: 0.00, 0.01, 0.05

USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT

root pts/0 192.168.56.1 05Apr17 0.00s 1.12s 0.05s w

root pts/1 192.168.56.1 06Apr17 10days 0.09s 0.09s -bash

\[root@oldboyedu35-nb ~\]\# uptime

10:34:02 up 1 day, 22:22, 2 users, load average: 0.00, 0.01, 0.05

\[root@oldboyedu35-nb ~\]\#

\[root@oldboyedu35-nb ~\]\# who

root pts/0 2017-04-05 12:15 \(192.168.56.1\)

root pts/1 2017-04-06 08:52 \(192.168.56.1\)

\[root@oldboyedu35-nb ~\]\# lastlog

Username Port From Latest

root pts/1 192.168.56.1 Sun Apr 16 10:37:58 +0800 2017

bin \*\*Never logged in\*\*

daemon \*\*Never logged in\*\*

adm \*\*Never logged in\*\*

lp \*\*Never logged in\*\*

sync \*\*Never logged in\*\*

shutdown \*\*Never logged in\*\*

halt \*\*Never logged in\*\*

mail \*\*Never logged in\*\*

uucp \*\*Never logged in\*\*

operator \*\*Never logged in\*\*

games \*\*Never logged in\*\*

gopher \*\*Never logged in\*\*

ftp \*\*Never logged in\*\*

nobody \*\*Never logged in\*\*

dbus \*\*Never logged in\*\*

vcsa \*\*Never logged in\*\*

abrt \*\*Never logged in\*\*

haldaemon \*\*Never logged in\*\*

ntp \*\*Never logged in\*\*

saslauth \*\*Never logged in\*\*

postfix \*\*Never logged in\*\*

sshd \*\*Never logged in\*\*

tcpdump \*\*Never logged in\*\*

oldboy \*\*Never logged in\*\*

junge \*\*Never logged in\*\*

alex \*\*Never logged in\*\*

oldgirl \*\*Never logged in\*\*

test \*\*Never logged in\*\*

kevin \*\*Never logged in\*\*

jason \*\*Never logged in\*\*

jason888 \*\*Never logged in\*\*

mysql \*\*Never logged in\*\*

alex666 \*\*Never logged in\*\*

jason007 \*\*Never logged in\*\*

oldboy888 \*\*Never logged in\*\*

oldboy666 \*\*Never logged in\*\*

\[root@oldboyedu35-nb ~\]\# \#\#\#\#登录----本地登录（输入用户名密码）或者远程登录 （xshell crt putty\)

