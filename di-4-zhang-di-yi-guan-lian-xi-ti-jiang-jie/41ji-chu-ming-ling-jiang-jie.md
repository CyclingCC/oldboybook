#### 1、linux命令操作语法

命令 \[参数选项\] \[ 文件或路径\]

| 命令 | 空格 | \[参数选项\] | 空格 | \[文件或路径\] |
| :--- | :--- | :--- | :--- | :--- |
| cat | 至少一个空格 | -n | 至少一个空格 | /etc/hosts |

#### 2、创建目录 mkdir

\[root@oldboy ~\]\# mkdir /data

##### 例子：

请用一条命令完成创建目录/oldboy/test，即创建/oldboy目录及/oldboy/test目录

\[root@oldboy ~\]\# mkdir /oldboy/test -p

#### 3、查看目录下的内容 ls

\[root@centos69 ~\]\# ls /data/

\[root@centos69 ~\]\# ls -l /data/

total 0

#### 4、查看目录本身 ls

\[root@centos69 ~\]\# ls -d /data/

/data/

\[root@centos69 ~\]\# ls -ld /data/

drwxr-xr-x 2 root root 4096 May 2 12:10 /data/

#### 5、切换目录 cd

\[root@oldboy ~\]\# cd /

#### 6、相对路径和绝对路径

##### 绝对路径：从/\(根\)开始的路径

cat /etc/sysconfig/network-scripts/ifcfg-eth0

##### 相对路径:不从/\(根\)开始

etc/sysconfig/network-scripts/

##### 例子：

\[root@oldboy /\]\# cd /etc &lt;==绝对路径

\[root@oldboy etc\]\# cd sysconfig/ &lt;==相对路径，相对于谁？相对于命令行里前面etc目录的

\[root@oldboy sysconfig\]\# cd /dev &lt;==绝对路径

\[root@oldboy sysconfig\]\# cd /data

#### 7、查看当前所在路径 pwd

\[root@oldboy data\]\# pwd

/data

#### 8、文件操作

在/data下面建立一个文件oldboy.txt

创建文件

\[root@oldboy data\]\# touch oldboy.txt

\[root@oldboy data\]\# ls

oldboy.txt

\[root@oldboy data\]\# touch /data/oldboy.txt

root@oldboy etc\]\# cd /data

\[root@oldboy data\]\# pwd

/data

\[root@oldboy data\]\# vi oldboy.txt

#### 9、cp命令

##### cp 拷贝文件或目录 默认只能拷贝文件

##### cp命令格式

cp \[OPTION\]... SOURCE... DIRECTORY

cp \[选项\] 文件（或目录）... 目录

cp \[OPTION\]... -t DIRECTORY SOURCE...

cp \[选项\] -t 目录 文件（或目录）...

##### 参数选项

-r \(递归\) 拷贝目录

-p 保持属性

-a 完全拷贝 相当于 -pdr

##### 例子：

##### i、把oldboy.txt文件拷贝到/tmp下

cp /data/oldboy.txt /tmp/

cp -r /data /tmp/

##### ii、已知/tmp下已经存在test.txt文件，如何执行命令才能把/mnt/test.txt拷贝到/tmp下覆盖掉/tmp/test.txt，而让系统不提示是否覆盖，cp不提示：

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

