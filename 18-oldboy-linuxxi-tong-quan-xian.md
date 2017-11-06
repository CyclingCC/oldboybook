# 第1章 系统权限

![](/assets/18-1.png)

### 1.1  权限位置说明

![](/assets/18-7.png)

### 1.2  权限设置

![](/assets/18-8.png)![](/assets/18-9.png)

### 1.3  普通文件的读、写、执行权限

1、可读r：表示具有读取/阅读文件内容的权限

2、可写w：表示具有新增、修改文件内容的权限

1）如果没有r配合，那么vi编辑文件会提示无法编辑（但可强制编辑），echo可以重定向或追加

2）特别提示：删除文件（修改文件名等）的权限是受父目录的权限控制，和文件本身权限无关

3、可执行x：表示具有执行文件的权限

1）文件本身要能够执行

2）普通用户同时还需要具备r的权限才能执行

3）root只要有x的权限就能执行

### 1.4  目录的读、写、执行权限

1、可读r：表示具有浏览目录下面文件及子目录的权限，即可以执行ls  dir

```
1）如果没有x权限，则不能进到目录里，即无法执行cd  dir

2）如果没有x权限，ls列表时可以看到所有文件名，但是会提示无权访问目录下文件

3）如果ls -l列表，所有的属性会带有问号，也会提示无权访问目录下文件，但是可以看到所有            文件名
```

2、可写w：表示具有增加 、删除、或修改目录内文件名（一般指文件名）的权限（需要x权限配合）

3、可执行x：表示具有进入目录的权限   例如可以执行cd  dir

但是没有r则无法列表文件及目录，没有w无法新建和删除文件名

| **权限** | **针对文件** | **针对目录** |
| :--- | :--- | :--- |
| --- | 什么都做不了 | 什么都做不了 |
| r-- | 可以查看文件内容 | 只能看到文件名 |
| -w- | 对文件写操作会覆盖文件内容 | 什么都做不了 |
| --x | 什么都做不了 | 可以cd |
| rw- | 正常读写 | 只能查看文件名 |
| r-x | 可读可执行 | 可以cd可以查看 |
| -wx | 对文件写操作会覆盖文件内容 | 可以cd可以写不能查看 |
| rwx | 什么都可以做 | 什么都可以做 |

### 1.5 权限测试三步

\#第一步-看看你是谁？

\#第二步-你和这个文件的关系（用户？ 一个组？ 其他人？ ）

\#第三步-权限

### 1.6  测试环境

\[root@oldboy oldboy\]\# groupadd incahome

\[root@oldboy oldboy\]\# usermod -g incahome oldboy

\[root@oldboy oldboy\]\# id oldboy

uid=500\(oldboy\) gid=501\(incahome\) 组=501\(incahome\)

\[root@oldboy oldboy\]\# useradd test

\[root@oldboy oldboy\]\# mkdir /oldboy -p

\[root@oldboy oldboy\]\# echo "echo oldboylinux" &gt;/oldboy/test.sh

\[root@oldboy oldboy\]\# chmod +x /oldboy/test.sh

\[root@oldboy oldboy\]\# cat /oldboy/test.sh

### 企业面试题：请从linux文件系统的角度详细描述读取/oldboy/test.sh文件的过程。

\[root@oldboy oldboy\]\# chmod u=-,g=x,o=w test/oldboy.sh

\[root@oldboy oldboy\]\# ls -l test

总用量 0

------x-w- 1 root root 0 3月  21 02:06 gongli.txt

------x-w- 1 root root 0 3月  21 02:03 oldboy.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod u=-,g=x,o=w test/oldgirl.sh

\[root@oldboy oldboy\]\# ls -l test

总用量 0

------x-w- 1 root root 0 3月  21 02:06 gongli.txt

------x-w- 1 root root 0 3月  21 02:03 oldboy.sh

------x-w- 1 root root 0 3月  21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod g+w test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-----wx-w- 1 root root 0 3月  21 02:06 gongli.txt

------x-w- 1 root root 0 3月  21 02:03 oldboy.sh

------x-w- 1 root root 0 3月  21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod u=rx,g-w,o=rx test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-x--xr-x 1 root root 0 3月  21 02:06 gongli.txt

------x-w- 1 root root 0 3月  21 02:03 oldboy.sh

------x-w- 1 root root 0 3月  21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod a-x test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-----r-- 1 root root 0 3月  21 02:06 gongli.txt

------x-w- 1 root root 0 3月  21 02:03 oldboy.sh

------x-w- 1 root root 0 3月  21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod -R a=rx test

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-xr-xr-x 1 root root 0 3月  21 02:06 gongli.txt

-r-xr-xr-x 1 root root 0 3月  21 02:03 oldboy.sh

-r-xr-xr-x 1 root root 0 3月  21 02:03 oldgirl.sh

-r-xr-xr-x 1 root root 0 3月  21 02:03 test.sh

\[root@oldboy oldboy\]\#

### 1.7  文件访问过程-详解

![](/assets/18-2.png)

# 第2章  默认权限

权限安全临界点

inux的默认权限就是安全的临界点，也是最佳的权限

目录 755  文件 644  是 相对安全的临界点

用户为root  用户组为root

![](/assets/18-3.png)

1、http协议 请求方法控制post，禁止get

2、挂载  noexec

3、程序前端控制 .jpg,zip

4、服务层，指定目录禁止php解析

![](/assets/18-4.png)

# 第3章  umask

##### 文件默认最大权限是666

##### 目录默认最大权限是777

控制默认权限 umask

root用户：umask（022）

其它用户：umask（002）

\[root@oldboy ~\]\# sed -n '61,69p' /etc/profile

if \[ $UID -gt 199 \] && \[ "\`id -gn\`" = "\`id -un\`" \]; then

umask 002

else

umask 022

fi

for i in /etc/profile.d/\*.sh ; do

if \\[ -r "$i" \\]; then

if \\[ "${-\\#\\*i}" != "$-" \\]; then

使用touch或mkdir命令创建文件或目录时的默认权限，通过umask修改

文件权限=系统内核文件默认权限-umask

644=666-022

目录权限=系统内核目录默认权限-umask

755=777-022

修改umask的值：

umask 数字

### 3.1  文件默认权限控制

文件umask 最大值666

情况一：

666  -  022  =  644

666   最大值

022   umask   -

---

644

情况二：

666

033  umask

---

633

情况三：

633

011   +

---

644

##### 对于文件   umask值任意一位是奇数时，  减umask值  后，  对应位为奇数的  加1

### 3.2  目录默认权限控制

目录umask最大值777

777

022   -

755

# 第4章 特殊权限位

### 4.1 suid

4\(SUID\)  设置SUID的文件，无论谁执行此文件，他都有文件所有者的权限

-rws

##### SUID 权限仅对二进制程序\(binary program\)有效

##### 执行者对于该程序需要具有x的可执行权限；

##### 本权限仅在执行该程序的过程中有效 \(run-time\)；

##### 执行者将具有该程序拥有者 \(owner\) 的权限。

查看系统有suid权限的命令：

find / -type f -perm 4755 \|xargs ls -l

Linux系统基本优化，取消无用的suid命令

文件有执行权限，不一定可以执行，还有内核控制

\[root@oldboy ~\]\# ll /usr/bin/passwd

-rwsr-xr-x. 1 root root 30768 2月  22 2012 /usr/bin/passwd

用户删除本来无权限的文件：（三个，满足一个即可）

a、 sudo 给 用户授权rm

b、给rm命令设置suid

c、设置上级目录w权限

\[root@oldboy test\]\# chmod u+s a.sh

\[root@oldboy test\]\# ll

total 0

-rwSr--r-- 1 root root 0 Sep  6 01:22 a.sh

\[root@oldboy test\]\# chmod u+x a.sh

\[root@oldboy test\]\# ll

total 0

-rwsr--r-- 1 root root 0 Sep  6 01:22 a.sh

### 4.2 sgid

2\(SGID\)   设置SGID的目录，无论谁来此目录，他都有目录所属组的权限

\[root@oldboy ~\]\# ll \`which locate\`

-rwx--s--x. 1 root slocate 38464 3月  12 2015 /usr/bin/locate

![](/assets/18-5.png)

##### SGID 可以针对目录来设置，目录设置sgid后，普通用户放到这个目录下的文件的用户组跟这个目录走

##### SGID 对二进制程序有用

##### 程序执行者对于该程序来说，需具备 x的权限

##### 执行者在执行的过程中将会获得该程序群组的支持

\[root@oldboy test\]\# ll

total 0

-rw-r--r-- 1 root root 0 Sep  6 01:22 a.sh

\[root@oldboy test\]\# chmod g+s a.sh

\[root@oldboy test\]\# ll

total 0

-rw-r-Sr-- 1 root root 0 Sep  6 01:22 a.sh

\[root@oldboy test\]\# chmod g+x a.sh

\[root@oldboy test\]\# ll

total 0

-rw-r-sr-- 1 root root 0 Sep  6 01:22 a.sh

### 4.3 sticky（粘滞位）

##### 存放在该目录的文件只允许属主操作

rwt  t代表设置了粘滞位

![](/assets/18-6.png)

tmp经典的粘滞位目录案例，特点，谁都有写权限，因此安全成问题，常常是木马第一手的跳板地点

linux高级优化，tmp目录常常是木马第一手跳板地点

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwt. 3 root root 10829824 Sep  6 00:41 /tmp

\[root@oldboy ~\]\# chmod o-t /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwx. 3 root root 10829824 Sep  6 00:41 /tmp

\[root@oldboy ~\]\# chmod o+t /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwt. 3 root root 10829824 Sep  6 00:41 /tmp

\[root@oldboy ~\]\# chmod o-x /tmp

\[root@oldboy ~\]\# ll -d /tmp

drwxrwxrwT. 3 root root 10829824 Sep  6 00:41 /tmp

### 4.4 设置特殊权限位

chmod  4755  filename

chmod  u+s filename

chmod  g+s filename

chmod  +t  /tmp

# 第5章 文件锁定

### 5.1 文件锁定：

\[root@oldboy ~\]\# chattr +i /etc/passwd

-a  文件内容只能增加

\[root@oldboy ~\]\# chattr +a /etc/passwd

### 5.2 文件解锁：

\[root@oldboy ~\]\# chattr -i /etc/passwd

查看文件锁定情况：

\[root@oldboy ~\]\# lsattr /etc/passwd

----i--------e- /etc/passwd

### 5.3 主要内容小结：

1、linux的9位权限及rwx字符的作用、对应数字及对应的用户和用户组图解

2、linux文件的权限说明

rwx对于文件来说代表什么意思。

3、linux目录的权限说明。

rwx对于目录来说代表什么意思。

4、企业生产场景网站目录设置权限的原则。

单台服务器网站权限控制方案（upload服务器）

集群服务器网站权限控制方案（上传、WEB、静态服务）

5、umask的作用以及和文件、目录的对应的默认权限关系。

特殊权限

6、suid是什么、作用，passwd命令案例，rm。做了小结了。

7、sgid是什么、作用，文件locate案例。共享目录用户组案例。

8、粘滞位是什么、作用，/tmp目录案例。

9、以数字及字符方式更改权限，chmod命令。

10、更改文件用户和组，chown命令。

11、更改用户组的，chgrp，大家多学习。不然被开发取代了。

12、chattr,lsattr更改文件属性。

13、setfacl知识不需要了解。

# 第6章  用户权限ACL访问控制列表

ACL:访问控制列表   可以为单独用户或单独组设置权限

setfacl  设置acl权限

getfacl  查看acl权限

mask  掩码

umask  反掩码

创建文件或目录时的默认权限 = 全权限掩码 - 反掩码

文件全权掩码  666

目录全权掩码  777

### 6.1  启用ACL

法1：临时开启

mount -o remount,acl /

法2：永久开启

tune2fs -o acl /dev/sda1

### 6.2 设置ACL权限

\#setfacl -\[mbx\] &lt;rules&gt; &lt;filename&gt;

-m 添加或修改文件

-x 删除一个acl

-b 删除全部acl

setfacl  -m  u:用户名:权限  目录或文件名

```
        g

        o
```

setfacl -m u:u1:7  目录或文件名

setfacl -x u:u1 目录或文件名

设置ACL后，文件权限后面多个加号

如：rwxr-xr-x+

查看ACL情况：

getfacl  目录或文件名

\[root@oldboy ~\]\# ll a.txt

-rw-r--r-- 1 root root 73 Aug 30 16:54 a.txt

\[root@oldboy ~\]\# getfacl a.txt

\# file: a.txt

\# owner: root

\# group: root

user::rw-

group::r--

other::r--

\[root@oldboy ~\]\# setfacl -m u:oldboy:rwx a.txt

\[root@oldboy ~\]\# getfacl a.txt

\# file: a.txt

\# owner: root

\# group: root

user::rw-

user:oldboy:rwx

group::r--

mask::rwx

other::r--

\[root@oldboy ~\]\# ll a.txt

-rw-rwxr--+ 1 root root 73 Aug 30 16:54 a.txt

ACL 对文件/目录的访问控制列表 超越rwx权限，更细化的定义权限

# 第7章 chown 修改文件所有者和所属组

chown 【选项】...  \[所有者\]\[:\[组\]\] 文件

chown   用户   文件或目录

chown  :组    文件或目录

chown  用户:组  文件或目录

chown  用户.组  文件或目录

# 第8章  附加

chmod 没了x权限

1.别的机器上面复制回来

2.install -m 755 /bin/chmod /tmp/chmod   \#\#权限回来了，在复制回去即可。

