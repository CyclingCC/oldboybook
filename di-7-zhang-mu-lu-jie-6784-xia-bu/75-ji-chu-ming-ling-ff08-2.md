#### 1、sed 三剑客老二 擅长取行 查找替换

##### 参数

-n  '从哪里来,到哪里去p' 取消默认输出

-i    修改文件内容

sg  查找替换

s查找

g全局/全部查找替换

-n 取消默认输出 sed默认输出整个文件的内容

##### 例子：

```
sed -n '20,30p' ett.txt
find /oldboy/ -type f -name "*.sh"|xargs sed -i 's#oldboy#oldgirl#g'
```

#### 2、awk 三剑客老大 擅长取列

##### 参数：

NR  表示行号

&&  并且

数字 取文件中的第几列

＄0   取出文件的第一整行

$NF     取出最后一列

-F "\[ ,\]" 指定菜刀 空格或者逗号（,）

awk 默认的菜刀是空格或连续的空格 tab符号

##### 例子：

```
awk ‘NR<=30’/data/ett.txt
awk ‘NR<=30 && NR>=20’/data/ett.txt
awk '{print NR,$0}' nginx.conf  $0 显示第一列
[root@oldboy35-moban data]# awk '{print NR,$0}' nginx.conf 
1 std1
2 std2
3 std3
4 std4
5 std5
[root@oldboyedu oldboy]# awk -F "[ ,]" '{print $3,$NF}' oldboy.txt 
oldboy 31333741
```

#### 3、tail 尾巴 取文件的后面几行\(默认取文件的最后10行\)

##### 参数：

-n 数字 -数字 tail -n1 === tail -1

-f 实时显示文件内容的更新

##### 例子：

```
[root@oldboy35-moban ~]# awk ‘NR<=30’/data/ett.txt |tail -11
```

#### 4、 alias 设置或者显示别名

1）第一个里程碑-如何显示出这句话

```
[root@oldboy35-moban ~]# echo do not use rm command.
do not use rm command.
```

2）第二个里程碑-rm与echo命令直接如何拉一根红线  宗旨 ： 照葫芦画瓢  照猫画虎

```
[root@oldboyedu-35 ~]# alias 
alias cp='cp -i'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

3）第三个里程碑-模仿

```
[root@oldboyedu-35 ~]# #给rm设置别名
[root@oldboyedu-35 ~]# #rm 显示 command not found 
[root@oldboyedu-35 ~]# #1.如何显示command not found
[root@oldboyedu-35 ~]# echo command not found 
command not found
[root@oldboyedu-35 ~]# #2.如何设置这个别名
[root@oldboyedu-35 ~]# alias rm='echo command not found'
[root@oldboyedu-35 ~]# #alias 小名='命令'
```

4）第四个里程碑-瞅瞅-进行测试

```
[root@oldboyedu-35 ~]# #3.检查
[root@oldboyedu-35 ~]# alias 
alias cp='cp -i'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='echo command not found'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@oldboyedu-35 ~]# rm  /tmp/test.txt 
command not found /tmp/test.txt
[root@oldboyedu-35 ~]# rm  -fr  /tmp/test.txt 
command not found -fr /tmp/test.txt
```

5）第五个里程碑-写合同（写到文件中）-永久生效

```
/etc/profile  ##写在文件的末尾（echo "">>）
G (shift g) 到文件的最后一行
[root@oldboyedu-35 ~]# tail /etc/profile
        else
            . "$i" >/dev/null 2>&1
        fi
    fi
done
unset i
unset -f pathmunge
alias rm='echo command not found'
```

6）第六个里程碑-合同生效  重新登录

```
vim /root/.bashrc   #注释掉alias 这三行 
rm mv cp  ## /root/.bashrc 
# .bashrc
# User specific aliases and functions
#alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
```

7）如何查找命令放在哪里（绝对路径）

```
[root@oldboy35-moban ~]# which cp
/bin/cp
[root@oldboy35-moban ~]# which mkdir
/bin/mkdir
```

8）临时的取消了命令的别名

方法一：

```
\cp /mnt/test.txt /tmp
\ ===>转义字符  ===> \班长  ===>学生
```

方法二：

```
/bin/cp /mnt/test.txt
mv 也是
```

方法三：unalis（不推荐）

取消掉对应的别名

#### 5、seq 生成连续的数字\(生成数字序列\)

```
[root@oldboy35-moban ~]# seq 10 >a.txt
[root@oldboy35-moban ~]# cat a.txt
1
2
3
4
5
6
7
8
9
10
```

#### 6、uname 你的\(linux\)名字/信息

参数：

-r  kernel  显示内核版本

-m  显示32位或64位

版本信息查询

```
[root@oldboy35-moban oldboy]# cat /etc/redhat-release 
CentOS release 6.8 (Final)
[root@oldboy35-moban ~]# uname 
Linux
[root@oldboy35-moban ~]# uname -r
2.6.32-642.el6.x86_64
[root@oldboy35-moban ~]# uname -m
x86_64
```

#### 7、useradd 用户名  添加用户名

参数：

-s 指定一个用户使用的命令解释器（shell）

/bin/bash

/sbin/nologin   傀儡用户

-u uid 指定用户的uid

-g 指定用户属于的初始组

-G 指定用户属于其他的组（附加）

-c coment 注释信息

-d 指定一个用户的家目录

-s 指定用户的命令解释器（shell）

```
[root@oldboy35-moban ~]# useradd oldgirl
```

#### 8、passwd 修改/设置密码（默认修改当前用户的密码）

参数：

--stdin  非交互式设置密码（从管道中获取密码）

例子：

```
echo 123456 |passwd --stdin oldboy
Changing password for user oldboy.
passwd: all authentication tokens updated successfully.
[root@oldboyedu-35 ~]# passwd oldboy
Changing password for user oldboy.
New password:                                   ###输入一个新的密码
BAD PASSWORD: it is too simplistic/systematic   ###密码太简单了
Retype new password:                            ###确认密码（在输入一次密码）
```

#### 9、whoami 显示当前用户的用户名字

例子：

```
[root@oldboy35-moban ~]# whoami
root
```

#### 10、setenforce 临时修改selinux的状态

\#数字0表示Permissive，即给出警告提示，但不会阻止操作，相当于disabled。

\#数字1表示Enforcing，即表示SElinux为开启状态。

getenforce 查看selinux的状态

\#\#\#命令行 临时

```
[root@oldboyedu-35 ~]# getenforce 
Enforcing
[root@oldboyedu-35 ~]# setenforce 
usage:  setenforce [ Enforcing | Permissive | 1 | 0 ]
[root@oldboyedu-35 ~]# setenforce 0
[root@oldboyedu-35 ~]# getenforce 
Permissive
```

\#\#\#文件中更改，永久生效

第一步 操作前的备份\(复制\)：

```
[root@oldboy35-moban ~]# cp /etc/selinux/config /etc/selinux/config.bak
```

第二步 cat看一眼 找目标

```
[root@oldboy35-moban ~]# cat /etc/selinux/config
[root@oldboy35-moban ~]# sed 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/selinux/config
```

第三步 成功后加-i替换

```
[root@oldboy35-moban ~]# sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/selinux/config
```

第四步查看

```
[root@oldboyedu-35 ~]# grep "=disabled" /etc/selinux/config
SELINUX=disabled
[root@oldboy35-moban ~]# cat /etc/selinux/config
```

#### 11、chkconfig  linux管理开机自启动软件\(服务\)

参数：

--list   显示所有软件的开机自启动状态

--level  指定运行级别 后边加数字

chkconfig iptables off 关闭

chkconfig iptables on  开启

彻底的让一个服务，不再运行

1. 关闭当前正在运行的进程（服务）=====&gt;/etc/init.d/iptables stop

2. 让他在开机不启动======&gt;chkconfig iptables off

例子：

```
[root@oldboyedu-35 ~]# chkconfig |grep ipt
iptables        0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@oldboyedu-35 ~]# chkconfig |grep iptables
iptables        0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@oldboy35-moban data]# chkconfig --level 3 iptables on
[root@oldboy35-moban data]# chkconfig --list iptables
iptables           0:off    1:off    2:off    3:on    4:off    5:off    6:off
```

#### 12、 source 让配置文件生效

可以用source生成的文件

/etc/profile

/etc/sysconfig/i18n

#### 13、 mount 挂载命令 把苹果\(磁盘\) 挂载到苹果树\(目录\)上

```
[root@oldboy35-moban ~]# mount /dev/cdrom /mnt/
mount: block device /dev/sr0 is write-protected, mounting read-only
```

#### 14、umount 卸载 把苹果从树上拿下来

#### 15、df 磁盘的使用情况

参数：

-h --human-readable 人类可读，以尽可能让人类读懂

```
[root@oldboy35-moban dev]# df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       6.9G  1.5G  5.1G  23% /
tmpfs           931M     0  931M   0% /dev/shm
/dev/sda1       190M   38M  142M  22% /boot
/dev/sr0        3.7G  3.7G     0 100% /mnt
[root@oldboyedu35-nb ~]# df -h
Filesystem（文件系统 分区 苹果）      Size  Used Avail Use% Mounted on（挂载点 树枝）
/dev/sda3       6.9G  1.7G  4.9G  25% /
tmpfs           491M     0  491M   0% /dev/shm
/dev/sda1       190M   34M  147M  19% /boot
```

#### 16、tree 以树的形状显示目录结构

参数：

-L 1 最多显示几层目录

-d   只显示目录

例子：

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
yum install -y tree
```

17、ifconfig 查看网卡ip地址\(位置\)

例子：

\[root@oldboy35-moban ~\]\# ifconfig

eth0      Link encap:Ethernet  HWaddr 00:0C:29:D2:B3:01  

          inet addr:192.168.56.128  Bcast:192.168.56.255  Mask:255.255.255.0

          inet6 addr: fe80::20c:29ff:fed2:b301/64 Scope:Link

          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

          RX packets:2447 errors:0 dropped:0 overruns:0 frame:0

          TX packets:2147 errors:0 dropped:0 overruns:0 carrier:0

          collisions:0 txqueuelen:1000 

          RX bytes:238398 \(232.8 KiB\)  TX bytes:283304 \(276.6 KiB\)



lo        Link encap:Local Loopback  

          inet addr:127.0.0.1  Mask:255.0.0.0

          inet6 addr: ::1/128 Scope:Host

          UP LOOPBACK RUNNING  MTU:65536  Metric:1

          RX packets:0 errors:0 dropped:0 overruns:0 frame:0

          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0

          collisions:0 txqueuelen:0 

          RX bytes:0 \(0.0 b\)  TX bytes:0 \(0.0 b\)



18、if up    启动某一个块/个网卡  

if down 关闭某一个块/个网卡 

例子：

/etc/init.d/network restart \#\#\#重启所有网卡 

   	if down eth0 && if up eth0    \#\#重启某一个网卡 \(down 不能单独使用否则跑机房\)

19、w   查看系统谁登陆了 在干啥   可以查看系统负载（繁忙程度）

\[root@oldboy35-moban ~\]\# w

 22:13:19 up  1:50,  2 users,  load average: 0.00, 0.01, 0.05

USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT

root     tty1     -                20:24    1:49m  0.15s  0.15s -bash

root     pts/0    192.168.56.1     21:01    1.00s  0.41s  0.24s w

20、free 查看系统内存的使用情况 

参数： 

-h  人类可读 

-m  以MB为单位显示

\[root@oldboy35-moban ~\]\# free -h

             total       used       free     shared    buffers     cached

Mem:          1.8G       293M       1.5G       228K        45M        85M

-/+ buffers/cache:       163M       1.7G

Swap:         767M         0B       767M

21、nl  显示文件内容及行号

\[root@oldboy35-moban data\]\# nl nginx.conf 

     1	std1

     2	std2

     3	std3

     4	std4

     5	std5



22、tar 打包压缩的命令

参数：zcvf 创建一个压缩包

z	 以gzip软件进行压缩包

c 	 create 创建\(压缩\)包

v 	 verbose 显示过程\(打包 压缩 解压过程\)

f 	 筐 file 指定压缩包名字\(尽量放到参数的最后\)



ztf 	查看压缩包内容

t list 列表 显示压缩包中的内容

zxvf   解压缩

xf

x 	   extract 解压缩 

--exclude= 排除 某个文件

--exclude-from= 根据一个列表\(文件\)，进行排除

-C 解压到指定位置

\[root@oldboy35-moban tmp\]\# tar zcvf /tmp/etc-paichu.tar.gz /etc/  打包压缩

\[root@oldboy35-moban tmp\]\# tar ztf /tmp/etc.tar.gz 查看压缩

\[root@oldboy35-moban tmp\]\#cd /tmp/

\[root@oldboy35-moban tmp\]\#tar zxvf /tmp/etc.tar.gz  解压缩

\[root@oldboy35-moban tmp\]\# ls

\[root@oldboy35-moban tmp\]\# pwd

\[root@oldboy35-moban tmp\]\# tar zcvf /tmp/etc-paichu.tar.gz /etc/  --exclude=etc/services 排除

\[root@oldboy35-moban tmp\]\# tar tf /tmp/etc-paichu.tar.gz \|grep services



23、cut 切割，取出你需要的某列 awk小弟，阉割版

参数：-d 指定菜刀

			-f 取出某一部分

			-f5		取出第五列

			-f1,5	取出第一列和第五列

			-f1-5 	取出第一列到第五列

			-c 取字符\(文本 字母\)  

\[root@oldboyedu oldboy\]\# cut  -d  " "    -f3,5  oldboy.txt \|sed 's\#,myqq \#,\#g'

24、wc 统计文件有多少行。

	-l 统计文件有多少行

\[root@oldboyedu oldboy\]\# wc -l /etc/services 

10774 /etc/services

25、dumpe2fs  显示文件系统（分区）的信息

inode size

block size

dumpe2fs /dev/sda3\|egrep -i "block size\|inode count"

\[root@oldboyedu35-nb ~\]\# dumpe2fs /dev/sda3 \|grep -i "inode size"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode size:	          256

26、last 显示用户登录信息

lastlog 显示所有用户的最近一次的登录信息

27、file查看文件的类型



