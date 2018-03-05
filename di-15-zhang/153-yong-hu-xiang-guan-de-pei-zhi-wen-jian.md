#### 1、/etc/default/useradd 文件 {#125-etcdefaultuseradd-文件}

useradd

/etc/defalut/useradd 文件时在使用useradd添加用户事放入一个需要调用的一个默认的配置文件，可以使用“useradd -D-\* 参数 ”，这样的命令格式来修改文件里面的内容

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

#### 2、与用户组相关的配置文件 {#113-与用户组相关的配置文件}

/etc/group \#--&gt;用户组配置文件

/etc/gshadow \#--&gt;用户组的影子文件

#### 3、/etc/login.defs（了解） {#126-etclogindefs（了解）}

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

#### 4、与usermod有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

#### 5、删除用户及用户相关的信息，与这个命令有关的文件有：

/etc/passwd 用户账号资料文件

/etc/shadow 用户账号资讯加密文件

/etc/group 用户组资讯文件

/etc/gshadow 用户组密码资讯文件

#### 练习题：

说出五个与用户相关的配置文件及对应的含义



