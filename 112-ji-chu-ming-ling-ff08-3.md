#### 1、ln 创建链接（创建硬链接）

参数：	

-s 创建软链接

```
[root@oldboyedu35-nb oldboy]# ln oldboy.txt oldboy.txt_hard 硬链接
[root@oldboyedu35-nb oldboy]# ln -s oldboy.txt oldboy.txt_soft 软链接
```

#### 2、tr 阉割版sed命令 替换

tr ","  "\n"  &lt;/oldboy/oldboy.txt

#### 3、stat 显示文件或目录信息

-c 以指定格式显示文件的信息

%a 以数字形式显示权限

```
stat -c %a /etc/hosts
```

#### 4、date 显示或修改时间日期

date +格式 以指定格式显示系统的时间或日期

%F === %Y-%m-%d  2017-03-27

%y                 17

%d		       27

%w               （0-6）

#### 5、which 找命令的位置

根据PATH的命令的位置 找命令

#### 6、locate 根据名字找文件，数据文件必须要更新

#### 7、whereis - 找命令，帮助文件（man），源代码

#### 8、shutdown 关闭或重启服务器

参数：

-h 关机	-h 时间

-r 重启   -r时间

-c 取消   将要进行的关机或重启

#### 9、reboot 重启

#### 10、关机

halt

poweroff

#### 11、chmod  修改文件的权限 

参数：

-R   递归的修改权限   目录及目录的子孙后代 

chmod 755 dir 

chmod +x test.sh

```
[root@oldboyedu35-nb oldboy]# chmod -R 644 oldboydir/
[root@oldboyedu35-nb oldboy]# ll -d oldboydir/
drw-r--r-- 2 oldboy incahome 4096 Mar 28 13:37 oldboydir/
[root@oldboyedu35-nb oldboy]# ls oldboydir/
oldboy.txt
[root@oldboyedu35-nb oldboy]# ll  oldboydir/
total 0
-rw-r--r-- 1 oldboy incahome 0 Mar 28 13:04 oldboy.txt
[root@oldboyedu35-nb oldboy]# ll test.sh 
-rw-r--r-- 1 oldboy root 17 Mar 28 13:36 test.sh
[root@oldboyedu35-nb oldboy]# chmod ugo+x test.sh 
[root@oldboyedu35-nb oldboy]# ll test.sh 
-rwxr-xr-x 1 oldboy root 17 Mar 28 13:36 test.sh
[root@oldboyedu35-nb oldboy]# chmod a-x test.sh 
[root@oldboyedu35-nb oldboy]# ll test.sh 
-rw-r--r-- 1 oldboy root 17 Mar 28 13:36 test.sh
[root@oldboyedu35-nb oldboy]# chmod +x test.sh 
[root@oldboyedu35-nb oldboy]# ll test.sh 
-rwxr-xr-x 1 oldboy root 17 Mar 28 13:36 test.sh
```

#### 12、chown 修改文件或目录的所有者和组

参数：-R 递归的修改

授权方法：

chown 用户 文件或目录 \#&lt;===仅仅授权用户

chown ：组 文件或目录 \#&lt;===仅仅授权组。等同于“chgrp组 文件或目录”

chown 用户:组 文件或目录 \#&lt;===表示授权用户和组

强调：

1）	其中的冒号“:”可以用点号“.”代替

2）	要授权的用户和组名，必须是linux系统里实际存在的

```
[root@oldboyedu35-nb oldboy]# chown oldboy.oldboy oldboy022
[root@oldboyedu35-nb oldboy]# ll 
total 20
-rwxr--r-x 1 oldboy oldboy      0 Mar 28 14:54 oldboy022
drwxr-xr-x 2 root   root     4096 Mar 28 14:55 oldboy022-dir
-rw-r--r-- 1 root   root        0 Mar 28 14:59 oldboy023
drwxr-xr-- 2 root   root     4096 Mar 28 14:59 oldboy023-dir
-rw-r---w- 1 root   root        0 Mar 28 15:08 oldboy034
drwxr---wx 2 root   root     4096 Mar 28 15:08 oldboy034-dir
drw-r--r-- 2 oldboy incahome 4096 Mar 28 13:37 oldboydir
---------- 1 oldboy root       17 Mar 28 13:36 test.sh
[root@oldboyedu35-nb oldboy]# chown oldboy oldboy023
[root@oldboyedu35-nb oldboy]# ll 
total 20
-rwxr--r-x 1 oldboy oldboy      0 Mar 28 14:54 oldboy022
drwxr-xr-x 2 root   root     4096 Mar 28 14:55 oldboy022-dir
-rw-r--r-- 1 oldboy root        0 Mar 28 14:59 oldboy023
drwxr-xr-- 2 root   root     4096 Mar 28 14:59 oldboy023-dir
-rw-r---w- 1 root   root        0 Mar 28 15:08 oldboy034
drwxr---wx 2 root   root     4096 Mar 28 15:08 oldboy034-dir
drw-r--r-- 2 oldboy incahome 4096 Mar 28 13:37 oldboydir
---------- 1 oldboy root       17 Mar 28 13:36 test.sh

[root@oldboyedu35-nb /]# chown -R oldboy.oldboy /oldboy
[root@oldboyedu35-nb /]# ll /oldboy
total 20
-rwxr--r-x 1 oldboy oldboy    0 Mar 28 14:54 oldboy022
drwxr-xr-x 2 oldboy oldboy 4096 Mar 28 14:55 oldboy022-dir
-rw-r--r-- 1 oldboy oldboy    0 Mar 28 14:59 oldboy023
drwxr-xr-- 2 oldboy oldboy 4096 Mar 28 14:59 oldboy023-dir
-rw-r---w- 1 oldboy oldboy    0 Mar 28 15:08 oldboy034
drwxr---wx 2 oldboy oldboy 4096 Mar 28 15:08 oldboy034-dir
drw-r--r-- 2 oldboy oldboy 4096 Mar 28 13:37 oldboydir
---------- 1 oldboy oldboy   17 Mar 28 13:36 test.sh
```

#### 13、ps process 查看进程 

参数： ps -ef  查看系统上的每个进程

```
[root@oldboy35-moban ~]# ps -ef |grep sshd
root       1542      1  0 Mar30 ?        00:00:00 /usr/sbin/sshd
root       3733   1542  0 08:36 ?        00:00:02 sshd: root@pts/0 
root       4603   1542  0 11:58 ?        00:00:00 sshd: root@pts/1 
root       5346   4607  0 14:31 pts/1    00:00:00 grep --color=auto sshd
```

#### 14、id   查看用户的信息 uid gid 属于哪家的

```
[root@oldboyedu-35 ~]# id
uid=0(root) gid=0(root) groups=0(root) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

#### 15、 lsof  list open files 显示出系统中所有被打开的文件

```
[root@oldboyedu35-nb ~]# lsof |grep oldboy.txt

COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME

vim 3367 root 4u REG 8,3 12288 145536 /oldboy/.oldboy.txt.swp
```

谁在使用这个文件

命令

lsof \|grep delete





