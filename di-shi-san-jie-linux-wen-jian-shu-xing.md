第1章 文件属性概况

\[root@oldboy36 ~\]\# ll -i /etc/hosts

 

第一列    inode索引节点（相当于人的身份证号），系统读取文件时先通过文件名找到inode号，然后才能读取文件内容

第二列    文件类型及权限（第二列共11个字符：其中第一个字符是文件类型，随后的9个字符为文件的对应权限，最后一个字符点号 . 是和selinux有关的一个标识）

第三列    硬链接个数

第四列    文件或目录的所有者（属主）

第五列    文件或目录所属的组（属组）

第六列    文件或目录的大小

第七、八、九列    文件或目录内容的修改时间

第十列    文件名或目录名

注：文件名不是文件的属性，而是目录的内容

第2章 inode 和 block

索引节点，在格式化文件系统（ext2、ext3、ext4）生成的inode（身份证号） （存放文件属性，不包含文件名（姓名） ）和  block（存放文件内容）

inode号是文件在磁盘上的唯一标识

inode 用来存放文件的属性，它是指向文件的一个指针

格式化的本质就是创建文件系统

文件系统包括inode  和  block

inode  用来存放文件属性 用来找到block    inode 默认大小 256B

block  用来存放数据，block默认大小  有  1k 、 2k 、 4k

2.1  找文件的过程

首先找到文件名，找到文件名就知道它的inode号，通过inode可以找到文件内容的存放位置（block的位置），也就找到了文件的内容

文件名 在 它所在目录的block里面

2.2 查看设备信息：

dumpe2fs /dev/sda1

2.3 查看文件inode

\[root@oldboy /\]\# ls -i

150937 abc         2 boot       12 etc        11 lost+found  130063 opt   390148 selinux   150914 tmp

132550 app    150909 data   390153 home   130062 media            1 proc  130064 srv       130054 usr

12239 a.txt  150910 data1  390154 lib      1856 mnt         130051 root       1 sys       260098 var

390152 bin         4 dev    390149 lib64  150965 oldboy      390158 sbin   12238 test.txt

\[root@oldboy /\]\# stat /etc/hosts

File: "/etc/hosts"

Size: 192             Blocks: 8          IO Block: 4096   普通文件

Device: 803h/2051d      Inode: 40          Links: 2

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2016-03-20 16:53:44.467984719 +0800

Modify: 2016-03-13 23:14:28.528957412 +0800    文件内容

Change: 2016-03-13 23:14:28.539956838 +0800    文件属性

\[root@oldboy /\]\# dumpe2fs  /dev/sda3\|grep -i "inode size"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode size:               256

2.4 查看磁盘inode：

\[root@oldboy ~\]\# df -i

Filesystem     Inodes IUsed  IFree IUse% Mounted on

/dev/sda3      515088 55967 459121   11% /

tmpfs          126557     1 126556    1% /dev/shm

/dev/sda1       51200    38  51162    1% /boot

\[root@oldboy36 ~\]\# dumpe2fs /dev/sda1 \|grep -i "^inode"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              51200

Inodes per group:         2048

Inode blocks per group:   256

Inode size:               128

2.5 查看磁盘block：

\[root@oldboy ~\]\# df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/sda3       7.7G  1.5G  5.8G  20% /

tmpfs           495M     0  495M   0% /dev/shm

/dev/sda1       190M   36M  145M  20% /boot

\[root@oldboy36 ~\]\# dumpe2fs /dev/sda1 \|grep -i "^block"

dumpe2fs 1.41.12 \(17-May-2010\)

Block count:              204800

Block size:               1024

Blocks per group:         8192

磁盘满的标志 ：inode满 或者  block满

2.6  同时查看inode和block

dumpe2fs /dev/sda3 \|egrep -i "^\(inode\|block\) \(size\|count\)"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              262144

Block count:              1048576

Block size:               4096

Inode size:                  256

2.7 inode特点

1、磁盘被分区并格式化为ext4文件系统后生成一定数量的inode和block

2、inode 索引节点，存放文件的属性信息以及作为文件的索引（指向文件的实体）

3、ext3、ext4文件系统的block存放的是文件的实际内容

4、inode是磁盘上的一块存储空间，C6非启动分区inode默认大小256字节，C5是128字节

5、inode的表现形式是形式一串数字，不同的文件对应的inode在文件系统里是唯一的

6、inode节点号相同的文件，互为硬链接文件，可以认为是一个文件的不同入口

7、ext3、ext4文件系统下，一个文件至少要占用一个inode和一个block

8、ext3、ext4文件系统下，正常情况一个文件占用且只能占用一个inode

9、block是用来存储实际数据的，每个block的大小一般有1k 2k 4k几种，其中引导分区等为1k，其他普通分区多为4k

10、如果一个文件很大，需要占用多个block，如果文件很小，至少占用一个block，并且这个block剩余空间就浪费了

11、inode大小和总量查看：

\[root@oldboy ~\]\# dumpe2fs /dev/sda3 \|egrep -i 'block size\|Inode size'

dumpe2fs 1.41.12 \(17-May-2010\)

Block size:               4096

Inode size:               256

\[root@oldboy ~\]\# dumpe2fs /dev/sda3 \|egrep -i 'block count\|Inode count'

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              515088

Block count:              2057984

Reserved block count:     102899

注意：默认 block count 一般会大于 inode count 的数量

12、查看inode的总量和使用量

df  -i

13、查看文件的inode信息方法

ls -li  或 stat /etc/hosts

14、如何生成及指定inode大小

格式化命令 ： mkfs.ext4 -b 2048 -I 256 /dev/sdb

2.8  block特点

1、磁盘读取数据是按block为单位读取的

2、一个文件可能占用多个block 美读取一个block就会消耗一次磁盘I/O

3、如果要提升磁盘IO性能，那么就要尽可能一次性读取数据尽量的多

4、一个block只能存放一个文件的内容，无论内容有多少。如果block默认是4K大小，那么存放一个1K的文件，剩余3K就不能存放其他文件，只能浪费了

5、block并非越大越好，block太大对于存放小文件就会浪费磁盘空间

6、根据业务需求，确定默认的block大小，如果大文件（大于16K），一般设置block大一点，小文件（小于1k），一般设置block小一点

7、block太大，例如4k，文件都是0.1k的，大量浪费磁盘空间，但是访问性能高

8、block太小，例如1k，文件都是1000k，消耗大量磁盘IO

9、block大小设置也是格式化分区时候确定的，命令 mkfs.ext4 -b 2048 -I 256 /dev/sdb

10、企业里文件都会比较大（一般会大于4k），block设置大一些会提升磁盘访问效率

11、ext3/ext4文件系统（CentOS5和6），一般都设置为4k

当前的生产环境一般设置为4k 特殊的业务，如视频可以加大block大小

2.9  磁盘空间满

inode 使用完 或者 block使用完

inode满的原因   /var/spool/postfix/maildrop/  这个目录下小文件太多

1、磁盘被分区格式化制作文件系统后，会分为inode和block两部分内容

2、inode存放文件的属性及指向文件实体的指针，文件名存放在上级目录的block里

3、访问文件过程  ：  文件名 -----&gt; inode ------&gt; block

4、inode一般默认大小256B，block大小 1，2，4k，默认4k， 注意，引导分区等特殊分区除外

5、通过df -i 查看inode的数量及使用情况，dumpe2fs /dev/sda3 查看inode及block的大小及数量

6、一个文件要至少占用一个inode和一个block，多个文件可以占用同一个inode（硬链接），相同文件

7、一个block只能被一个文件使用，如果文件很小block很大，剩余空间浪费，无法继续被其他文件使用

第3章 文件类型

```
 -type c         
          File is of type c:



          b      block \(buffered\) special



          c      character \(unbuffered\) special



          d      directory



          p      named pipe \(FIFO\)



          f      regular file



          l      symbolic link; this is never true if the -L

                 option  or the -follow option is in effect,

                 unless the symbolic link is broken.  If you

                 want  to  search for symbolic links when -L

                 is in effect, use -xtype.



          s      socket



          D      door \(Solaris\)
```

文件类型标识符    文件类型说明

* 普通文件（文本文件、二进制文件、数据文件、压缩文件）

d    目录（directory）

l    软链接（link）

b    块设备（block）

c    字符设备（character）

s    socket文件

p    管道文件（pipe）

3.1  查看文件类型

\[root@oldboy36 ~\]\# file /etc/hosts

/etc/hosts: ASCII text

\[root@oldboy36 ~\]\# file /bin/ls

/bin/ls: ELF 64-bit LSB executable, x86-64, version 1 \(SYSV\), dynamically linked \(uses shared libs\), for GNU/Linux 2.6.18, stripped

\[root@oldboy36 ~\]\# file /var/log/wtmp

/var/log/wtmp: data

\[root@oldboy36 ~\]\# file etc.tar.gz

etc.tar.gz: gzip compressed data, from Unix, last modified: Thu May 11 15:00:02 2017

\[root@oldboy ~\]\# lastlog

用户名           端口     来自             最后登陆时间

root             pts/0    10.0.0.1         日 3月 27 08:59:46 +0800 2016

bin                                        \*\*从未登录过\*\*

daemon                                     \*\*从未登录过\*\*

adm                                        \*\*从未登录过\*\*

lp                                         \*\*从未登录过\*\*

sync                                       \*\*从未登录过\*\*

shutdown                                   \*\*从未登录过\*\*

第4章 文件权限

echo {0,1}{0,1}{0,1}

000 001 010 011 100 101 110 111

echo {0..1}{0..1}{0..1}

000 001 010 011 100 101 110 111

权限    r    w    x    -

含义    读    写    执行    没有任何权限

数字表示    4    2    1    0

设置权限的方法

方法1   数字表示

用户    组    其它

数字之和    数字之和    数字之和

r    w    x    r    w    x    r    w    x

方法2

u

g

o

a    +

-

=    r

w

x

第5章 链接

5.1  硬链接

硬链接：  具有相同inode号的文件（多个文件名对应一个inode号）互为硬链接

硬链接\(hard link, 也称链接\)就是一个文件的多个文件名。再说白点，所谓链接无非是把文件名和计算机文件系统使用的节点号链接起来。因此我们可以用多个文件名与同一个文件进行链接，这些文件名可以在同一目录或不同目录。

目录不能做硬链接

删除一个硬链接，仅仅删除了文件的链接指向

硬链接文件是文件的另一个入口

可以通过给文件创建硬链接文件，来防止重要文件被误删

删除文件的本质：文件的所有硬链接被删除，并且inode节点被其他文件占用

在父目录里创建一个子目录，父目录的链接数加1

硬链接小结

1、具有相同inode号的多个文件互为硬链接文件

2、删除硬链接文件或者删除源文件任意之一，文件实体不会删除

3、只有删除了源文件及所有的硬链接文件，文件实体才会被删除

4、当所有的硬链接及源文件被删除后，再存放新的数据会占用这个文件的空间，或者磁盘fsck检查的时候，删除的数据会被系统回收

5、硬链接文件就是一个文件的另一个入口

6、可以通过给文件设置硬链接，来防止重要文件被删除

7、通过执行命令  ln  源文件  硬链接文件   即可创建硬链接

8、硬链接是普通文件，可以使用rm命令删除

9、对于静态文件（没有进程正在调用的文件）来讲，硬链接数为0，文件就被删除

目录硬链接说明

\[root@oldboy test\]\# pwd

/test

\[root@oldboy test\]\# ls -ldi oldboy oldboy/. oldboy/oldboydir/..

398269 drwxr-xr-x 3 root root 4096 Aug 26 20:20 oldboy

398269 drwxr-xr-x 3 root root 4096 Aug 26 20:20 oldboy/.

398269 drwxr-xr-x 3 root root 4096 Aug 26 20:20 oldboy/oldboydir/..

5.2  软链接

软链接又叫符号链接，这个文件包含了另一个文件的路径名。可以是任意文件或目录，可以链接不同文件系统的文件 ,  linux软链接文件类似windows的快捷方式

软链接指向源文件名

软链接文件创建时，软链接的文件不能存在，如果存在，不能正确创建

软链接占用一个inode，不占用block

ln -s 源  目标

\[root@xdz application\]\# ln -s /application/apache2.2.17 /application/apache

\[root@xdz application\]\# ll

total 4

lrwxrwxrwx 1 root root   25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

查看软链接文件内容

\[root@xdz application\]\# readlink apache

/application/apache2.2.17

软链接小结

1、软链接类似windows的快捷方式

2、软链接类似一个文本文件，里面是源文件的路径。指向源文件实体

3、删除源文件、软链接文件依然存在、但是无法访问指向的源文件路径内容

4、失效的时候一般是白字红底闪烁提示

5、执行命令 “ln -s 源文件 软链接文件”，即可完成穿件软链接（目标不能存在）

6、软链接和源文件是不同类型的文件、也是不同的文件、inode号也不相同

7、删除软链接文件可以用rm命令

5.3  软硬链接的区别

1、软硬链接的概念

2、如何创建软硬链接

3、对文件软硬链接的区别

4、对目录软硬链接的区别

在linux系统中，链接分为两种：一个是硬链接，另一个是软链接（或符号链接）

1、默认不带参数情况下，ln命令创建的是硬链接，带-s参数的ln命令创建的是软链接

2、ln命令不能对目录创建硬链接，但可以创建软链接，对目录的软链接会经常用到

3、源文件和硬链接具有相同的inode号，是同一个文件

4、源文件和软链接inode号不同，是不同的文件，软链接相当于源文件的快捷方式，指向源文件

5、删除软链接文件，对源文件及硬链接文件无影响

6、删除文件的硬链接，对源文件及软链接文件无影响

7、删除源文件，对硬链接无影响，会导致软链接失效（红底白字闪）

8、同时删除源文件及硬链接，整个文件才会被真正的删除

9、对于目录，不可以人为创建，但可以创建软链接

10、对于目录的软链接是生产场景运维中常用的技巧

11、目录的硬链接不能跨越文件系统（从硬链接原理理解）

12、每个目录下面都有一个硬链接 “.”号，和对应上级目录的硬链接 “..”

13、在父目录里创建一个子目录，父目录的链接数加1（每个子目录里面都有..来指向父目录）

14、软链接可以跨文件系统，硬链接不可以跨文件系统

第6章  文件删除原理

rm 删除文件删除的只是文件名

控制文件删除：以下两个条件同时具备才生效

1、文件的硬链接数，有一个硬链接i\_link +1   减少一个硬链接，i\_link-1

2、是否有进程占用使用这个文件，有一个进程占用这个文件，i\_count+1

当没有进程调用时i\_count=0

当i\_link=0并i\_count=0时，文件被删除

文件删除，磁盘空间不释放的原因：

1、hardlink

2、另一个进程还在使用这个文件

3、磁盘空余空间维护出现问题

ln  源  目标

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 1 root root    0 Mar 26 11:16 a

lrwxrwxrwx 1 root root   25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

\[root@xdz application\]\# ln a b

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 2 root root    0 Mar 26 11:16 a

lrwxrwxrwx 1 root root   25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

-rw-r--r-- 2 root root    0 Mar 26 11:16 b

\[root@xdz application\]\# ln b c

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 3 root root    0 Mar 26 11:16 a

lrwxrwxrwx 1 root root   25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

-rw-r--r-- 3 root root    0 Mar 26 11:16 b

-rw-r--r-- 3 root root    0 Mar 26 11:16 c

\[root@xdz application\]\# ll -i

total 4

393238 -rw-r--r-- 3 root root    0 Mar 26 11:16 a

393237 lrwxrwxrwx 1 root root   25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

393236 drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

393238 -rw-r--r-- 3 root root    0 Mar 26 11:16 b

393238 -rw-r--r-- 3 root root    0 Mar 26 11:16 c

6.1  磁盘空间满了但是与du -sh 的结果不符---没有被彻底删除排查过程

第一个里程碑-什么原因：

\#\#\#\#已经删除了，但是空间没有释放

\#\#\#\#已经删除了-----把文件的硬链接数量为0

\#\#\#\#空间没有释放---还有人在使用---进程

第二个里程碑-排查方法：

\# lsof \|grep delete

rsyslogd  1250      root    1w      REG                8,3 1888889326     274029 /var/log/messages \(deleted\)

\#\#\#\#\#硬链接数为0了，但是还有一个rsyslog软件正在使用

\#\#\#这个文件没有被彻底删除

第三个里程碑-解决方法

\#\#重启对应的软件/服务即可

\# /etc/init.d/rsyslog restart

Shutting down system logger:                               \[  OK  \]

Starting system logger:                                    \[  OK  \]

第四个里程碑-检查结果

\# df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/sda3       8.8G  1.6G  6.8G  19% /

tmpfs           931M     0  931M   0% /dev/shm

/dev/sda1       190M   40M  141M  22% /boot

/dev/sdc         73K   14K   55K  21% /app/logs

第五个里程碑-总结

1.尽量清空日志文件不要删除

2.切割日志，删除旧的文件（几天以前的）

6.2  企业案例：如果向磁盘写入数据提示如下错误：No space left on device，通过df -h查看磁盘空间，发现没满，请问可能原因是什么？企业场景什么情况下会导致这个问题发生？

6.3  文件删除原理，进程调用文件，但是文件硬链接数为0，文件没有被释放 ，磁盘满故障

[http://oldboy.blog.51cto.com/2561410/612351](http://oldboy.blog.51cto.com/2561410/612351)

6.4  inode满案例2：因inode节点导致执行passwd命令报错处理记录

[http://blog.sina.com.cn/s/blog\_506ed9e6010106kj.html](http://blog.sina.com.cn/s/blog_506ed9e6010106kj.html)

第7章   用户和组

7.1  linux多用户多任务介绍

linux/unix是一个多用户、多任务的操作系统

7.2  用户UID  组GID

在linux系统中用户是分角色的，在linux系统中，由于角色不同，权限和完成的任务也不同；

注意：linux系统中，用户的角色是通过UID和GID识别的

UID是唯一标识一个系统用户帐号 用户名称是给人看的，linux系统只能识别UID和GID这样的数字

7.3  用户分类

UID    用户类型    用户特性

0    超级用户root    linux系统超级管理员，增加一个超级用户，只需要将UID改为0即可

1-499    虚拟用户    为了防止人为建立帐户的UID和系统UID冲突，这些用户不能登录

500-65535    普通用户    使用 useradd oldboy 建立帐户时，默认的UID就是从500开始的

7.4  linux安全优化

1、安装系统后可以删除用不到的虚拟用户，但最好不要删而是在配置文件中注释掉

2、部署服务时，也会创建虚拟用户，服务运行需要

7.5  查看用户信息

\[root@oldboy36 ~\]\# id oldboy

uid=500\(oldboy\) gid=500\(oldboy\) 组=500\(oldboy\)

7.6 用户相关配置文件

用户相关的文件：/etc/passwd、/etc/shadow、/etc/group、/etc/gshadow

/etc/passwd

root     :x            :0     :0      :root       :/root          :/bin/bash

用户名  :密码占位符   :UID   :GID   :用户说明  :用户家目录    :shell解释器

/etc/shadow

oldgirl:!!:17301:0:99999:7:::

oldgirl    用户名

:!!    加密的密码

:17301    从1970年1月1日起，到用户最近一次更改密码的天数

:0    从1970年1月1日起，到用户可以更改密码的天数

:99999    从1970年1月1日起，到用户必须更改密码的天数

:7    在用户密码过期前多少天提醒用户更改密码

:    在用户密码过期后到禁用账户的天数

:    从1970年1月1日起，到用户被禁用的天数（useradd -f）

:    保留

/etc/group

mail:x:12:mail,postfix

mail    :x             :12     :mail,postfix

组名    :密码占位符    :GID   :组成员

第8章  文件时间

ls -lhi

7 8 9 三列是时间（默认是修改时间）

modify  mtime  文件内容修改时间

change  ctime   文件属性改变时间

access   atime  文件内容访问时间

8.1  查看文件属性详细信息

\[root@oldboy36 ~\]\# stat /etc/hosts

File: "/etc/hosts"

Size: 158             Blocks: 8          IO Block: 4096   普通文件

Device: 803h/2051d      Inode: 654109      Links: 1

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2017-05-15 18:05:01.727193092 +0800

Modify: 2010-01-12 21:28:22.000000000 +0800

Change: 2017-05-01 12:07:24.733999989 +0800

