#### 1、文件删除原理

rm 删除文件删除的只是文件名

#### 2、控制文件删除：以下两个条件同时具备才生效

1、文件的硬链接数，有一个硬链接i\_link +1 减少一个硬链接，i\_link-1

2、是否有进程占用使用这个文件，有一个进程占用这个文件，i\_count+1

当没有进程调用时i\_count=0

当i\_link=0并i\_count=0时，文件被删除

#### 3、文件删除，磁盘空间不释放的原因

1、hardlink

2、另一个进程还在使用这个文件

3、磁盘空余空间维护出现问题

ln 源 目标

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 1 root root 0 Mar 26 11:16 a

lrwxrwxrwx 1 root root 25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

\[root@xdz application\]\# ln a b

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 2 root root 0 Mar 26 11:16 a

lrwxrwxrwx 1 root root 25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

-rw-r--r-- 2 root root 0 Mar 26 11:16 b

\[root@xdz application\]\# ln b c

\[root@xdz application\]\# ll

total 4

-rw-r--r-- 3 root root 0 Mar 26 11:16 a

lrwxrwxrwx 1 root root 25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

-rw-r--r-- 3 root root 0 Mar 26 11:16 b

-rw-r--r-- 3 root root 0 Mar 26 11:16 c

\[root@xdz application\]\# ll -i

total 4

393238 -rw-r--r-- 3 root root 0 Mar 26 11:16 a

393237 lrwxrwxrwx 1 root root 25 Mar 26 11:03 apache -&gt; /application/apache2.2.17

393236 drwxr-xr-x 2 root root 4096 Mar 23 23:41 apache2.2.17

393238 -rw-r--r-- 3 root root 0 Mar 26 11:16 b

393238 -rw-r--r-- 3 root root 0 Mar 26 11:16 c

#### 4、磁盘空间满了但是与du -sh 的结果不符---没有被彻底删除排查过程

##### 第一个里程碑-什么原因：

\#\#\#\#已经删除了，但是空间没有释放

\#\#\#\#已经删除了-----把文件的硬链接数量为0

\#\#\#\#空间没有释放---还有人在使用---进程

##### 第二个里程碑-排查方法：

\# lsof \|grep delete

rsyslogd 1250 root 1w REG 8,3 1888889326 274029 /var/log/messages \(deleted\)

\#\#\#\#\#硬链接数为0了，但是还有一个rsyslog软件正在使用

\#\#\#这个文件没有被彻底删除

##### 第三个里程碑-解决方法

\#\#重启对应的软件/服务即可

\# /etc/init.d/rsyslog restart

Shutting down system logger: \[ OK \]

Starting system logger: \[ OK \]

##### 第四个里程碑-检查结果

\# df -h

Filesystem Size Used Avail Use% Mounted on

/dev/sda3 8.8G 1.6G 6.8G 19% /

tmpfs 931M 0 931M 0% /dev/shm

/dev/sda1 190M 40M 141M 22% /boot

/dev/sdc 73K 14K 55K 21% /app/logs

##### 第五个里程碑-总结

1.尽量清空日志文件不要删除

2.切割日志，删除旧的文件（几天以前的）

#### 5、文件删除原理，进程调用文件，但是文件硬链接数为0，文件没有被释放 ，磁盘满故障

##### [http://oldboy.blog.51cto.com/2561410/612351](https://www.gitbook.com/book/cyclingcc/-linux/edit#)

#### ![](/assets/13-7.png)![](/assets/13-8.png)

#### 练习题：

1、文件删除的原理

2、磁盘空间满了但是与du -sh 的结果不符---没有被彻底删除排查过程

##### 



