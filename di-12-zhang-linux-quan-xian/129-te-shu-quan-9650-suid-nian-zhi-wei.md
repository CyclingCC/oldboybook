#### 1、suid

4\(SUID\) 设置SUID的文件，无论谁执行此文件，他都有文件所有者的权限

-rws

##### SUID 权限仅对二进制程序\(binary program\)有效 {#suid-权限仅对二进制程序binary-program有效}

##### 执行者对于该程序需要具有x的可执行权限； {#执行者对于该程序需要具有x的可执行权限；}

##### 本权限仅在执行该程序的过程中有效 \(run-time\)； {#本权限仅在执行该程序的过程中有效-run-time；}

##### 执行者将具有该程序拥有者 \(owner\) 的权限。 {#执行者将具有该程序拥有者-owner-的权限。}

#### 2、查看系统有suid权限的命令：

find / -type f -perm 4755 \|xargs ls -l

Linux系统基本优化，取消无用的suid命令

文件有执行权限，不一定可以执行，还有内核控制

\[root@oldboy ~\]\# ll /usr/bin/passwd

-rwsr-xr-x. 1 root root 30768 2月 22 2012 /usr/bin/passwd

用户删除本来无权限的文件：（三个，满足一个即可）

a、 sudo 给 用户授权rm

b、给rm命令设置suid

c、设置上级目录w权限

\[root@oldboy test\]\# chmod u+s a.sh

\[root@oldboy test\]\# ll

total 0

-rwSr--r-- 1 root root 0 Sep 6 01:22 a.sh

\[root@oldboy test\]\# chmod u+x a.sh

\[root@oldboy test\]\# ll

total 0

-rwsr--r-- 1 root root 0 Sep 6 01:22 a.sh

#### 3、sgid

2\(SGID\) 设置SGID的目录，无论谁来此目录，他都有目录所属组的权限

\[root@oldboy ~\]\# ll \`which locate\`

-rwx--s--x. 1 root slocate 38464 3月 12 2015 /usr/bin/locate

![](https://www.luffycity.com/linux-book/assets/18-5.png)

##### SGID 可以针对目录来设置，目录设置sgid后，普通用户放到这个目录下的文件的用户组跟这个目录走 {#sgid-可以针对目录来设置，目录设置sgid后，普通用户放到这个目录下的文件的用户组跟这个目录走}

##### SGID 对二进制程序有用 {#sgid-对二进制程序有用}

##### 程序执行者对于该程序来说，需具备 x的权限 {#程序执行者对于该程序来说，需具备-x的权限}

##### 执行者在执行的过程中将会获得该程序群组的支持 {#执行者在执行的过程中将会获得该程序群组的支持}

\[root@oldboy test\]\# ll

total 0

-rw-r--r-- 1 root root 0 Sep 6 01:22 a.sh

\[root@oldboy test\]\# chmod g+s a.sh

\[root@oldboy test\]\# ll

total 0

-rw-r-Sr-- 1 root root 0 Sep 6 01:22 a.sh

\[root@oldboy test\]\# chmod g+x a.sh

\[root@oldboy test\]\# ll

total 0

-rw-r-sr-- 1 root root 0 Sep 6 01:22 a.sh

### 4、sticky（粘滞位） {#43-sticky（粘滞位）}

##### 存放在该目录的文件只允许属主操作 {#存放在该目录的文件只允许属主操作}

rwt t代表设置了粘滞位

![](https://www.luffycity.com/linux-book/assets/18-6.png)

tmp经典的粘滞位目录案例，特点，谁都有写权限，因此安全成问题，常常是木马第一手的跳板地点

linux高级优化，tmp目录常常是木马第一手跳板地点

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwt. 3 root root 10829824 Sep 6 00:41 /tmp

\[root@oldboy ~\]\# chmod o-t /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwx. 3 root root 10829824 Sep 6 00:41 /tmp

\[root@oldboy ~\]\# chmod o+t /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwt. 3 root root 10829824 Sep 6 00:41 /tmp

\[root@oldboy ~\]\# chmod o-x /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwT. 3 root root 10829824 Sep 6 00:41 /tmp

#### 5、设置特殊权限位

chmod 4755 filename

chmod u+s filename

chmod g+s filename

chmod +t /tmp

