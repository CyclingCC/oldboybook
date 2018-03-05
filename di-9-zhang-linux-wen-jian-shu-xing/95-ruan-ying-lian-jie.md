### 一、软连接

![](/assets/13-9.png)

#### 1、怎么来的

ln -s  创建软连接

\[root@oldboyedu42-lnb oldboy\]\# ln -s oldboy.txt  oldboy.txt-soft

\[root@oldboyedu42-lnb oldboy\]\# ls -l oldboy.txt\*

-rw-r--r--. 1 root root 29 Nov 11 05:10 oldboy.txt

lrwxrwxrwx  1 root root 10 Nov 11 12:09 oldboy.txt-soft -&gt; oldboy.txt

#### 2、特点

1\#方便我们使用目录

\[root@oldboyedu42-lnb oldboy\]\# ls -l /etc/init.d

lrwxrwxrwx. 1 root root 11 Oct 16 12:38 /etc/init.d -&gt; rc.d/init.d

\[root@oldboyedu42-lnb oldboy\]\# ls -l /etc/init.d /etc/rc.local

lrwxrwxrwx. 1 root root 11 Oct 16 12:38 /etc/init.d -&gt; rc.d/init.d

lrwxrwxrwx. 1 root root 13 Oct 16 12:39 /etc/rc.local -&gt; rc.d/rc.local

\[root@oldboyedu42-lnb oldboy\]\# ls -l /etc/init.d /etc/rc.local  /etc/rc.sysinit

lrwxrwxrwx. 1 root root 11 Oct 16 12:38 /etc/init.d -&gt; rc.d/init.d

lrwxrwxrwx. 1 root root 13 Oct 16 12:39 /etc/rc.local -&gt; rc.d/rc.local

lrwxrwxrwx. 1 root root 15 Oct 16 12:39 /etc/rc.sysinit -&gt; rc.d/rc.sysinit

\[root@oldboyedu42-lnb oldboy\]\# ls -l /etc/init.d /etc/rc.local  /etc/rc.sysinit

#### 3、怎没的

源文件被删除的时候，会红底白字闪烁

#### 例子：

mkdir -p /application/nginx-1.12.0

创建软连接 /application/nginx

ln -s /application/nginx-1.12.0 /application/nginx

### 二、硬链接

![](/assets/13-10.png)![](/assets/13-11.png)

#### 1、含义

超市前后门，文件的入口（文件名）

在同一个分区中（文件系统）文件之间的inode号码一样，这些文件之间互为硬链接

#### 2、怎么来的 ln

\[root@oldboyedu42-lnb oldboy\]\# ln oldboy.txt oldboy.txt-hard

\[root@oldboyedu42-lnb oldboy\]\# ls -l oldboy.txt\*

-rw-r--r--. 2 root root 29 Nov 11 05:10 oldboy.txt

-rw-r--r--. 2 root root 29 Nov 11 05:10 oldboy.txt-hard

lrwxrwxrwx  1 root root 10 Nov 11 12:09 oldboy.txt-soft -&gt; oldboy.txt

#### 3、特点

1\#彻底删除一个文件，与这个文件有关的硬链接都删除

2\#只防止文件被误删除

3\#无法对目录创建硬链接，会跨越文件系统

#### 练习题：

1、软连接的由来及特点

2、硬链接的由来及特点

3、软硬连接的区别？



