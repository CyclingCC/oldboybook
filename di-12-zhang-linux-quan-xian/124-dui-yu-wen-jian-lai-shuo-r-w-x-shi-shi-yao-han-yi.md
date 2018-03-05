#### 1、创建环境

mkdir -p /oldboy

echo 'hostname' &gt; /oldboy/oldwang.sh

chown oldboy.oldboy  /oldboy/oldwang.sh

#### 2、文件的R权限

\#\#\#root 用户下面 修改权限  文件的r

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

-rw-r--r-- 1 oldboy oldboy 9 Nov  3 18:12 oldwang.sh

\[root@oldboyedu42-lnb oldboy\]\# chmod u=r oldwang.sh

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

-r--r--r-- 1 oldboy oldboy 9 Nov  3 18:12 oldwang.sh

\#\#\#oldboy用户测试

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

hostname

\[oldboy@oldboyedu42-lnb oldboy\]$ echo 'pwd' &gt;&gt;oldwang.sh

-bash: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ /oldboy/oldwang.sh

-bash: /oldboy/oldwang.sh: Permission denied

#### 3、文件的W权限

\#\#\#root 用户下面 修改权限  文件的w

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

-r--r--r-- 1 oldboy oldboy 9 Nov  3 18:12 oldwang.sh

\[root@oldboyedu42-lnb oldboy\]\# chmod u=w oldwang.sh

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

--w-r--r-- 1 oldboy oldboy 9 Nov  3 18:12 oldwang.sh

\#\#\#oldboy 用户

\[oldboy@oldboyedu42-lnb oldboy\]$ ll /oldboy/oldwang.sh

--w-r--r-- 1 oldboy oldboy 9 Nov  3 18:12 /oldboy/oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ cat /oldboy/oldwang.sh

cat: /oldboy/oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ echo 'pwd' &gt;&gt;oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ echo 'pwd' &gt;&gt;oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ echo 'pwd' &gt;&gt;oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ /oldboy/oldwang.sh

-bash: /oldboy/oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ vim oldwang.sh

~

~

~

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ ll oldwang.sh

w-r--r-- 1 oldboy oldboy 21 Nov  3 18:23 oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ vim oldwang.sh

alias rm

~

~

~

"oldwang.sh" 1L, 9C written

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

cat: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

cat: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

cat: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

cat: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ ll oldwang.sh

--wxr--r-- 1 oldboy oldboy 9 Nov  3 18:25 oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ vim oldwang.sh

~

~

~

~

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

ias rm

\[oldboy@oldboyedu42-lnb oldboy\]$ vim oldwang.sh

alias rm

pwd

~

~

~

~

"oldwang.sh" 2L, 13C written

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

alias rm

pwd

##### 小结：

对于文件的w权限

1.修改文件的内容，w权限需要有人r权限配合

2.如果没有r权限，使用vi/vim 修改文件内容 会导致源文件内容清空

#### 3、文件的X权限

\#\#\#root 用户下面 修改权限  文件的x

\[root@oldboyedu42-lnb oldboy\]\# chmod u=x oldwang.sh

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

---xr--r-- 1 oldboy oldboy 13 Nov  3 18:29 oldwang.sh

\#\#\#oldboy

\[oldboy@oldboyedu42-lnb oldboy\]$ ll oldwang.sh

---xr--r-- 1 oldboy oldboy 13 Nov  3 18:29 oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$ cat oldwang.sh

cat: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ echo 'pwd' &gt;&gt;oldwang.sh

-bash: oldwang.sh: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ /oldboy/oldwang.sh

bash: /oldboy/oldwang.sh: Permission denied

#### 4、文件的rx权限

\#\#\#root 用户下面 修改权限  文件的rx

\[root@oldboyedu42-lnb oldboy\]\# ll oldwang.sh

-r-xr--r-- 1 oldboy oldboy 13 Nov  3 18:29 oldwang.sh

\#\#\#oldboy

\[oldboy@oldboyedu42-lnb oldboy\]$ cat /oldboy/oldwang.sh

pwd

\[oldboy@oldboyedu42-lnb oldboy\]$ /oldboy/oldwang.sh

/oldboy

\[oldboy@oldboyedu42-lnb oldboy\]$ ll /oldboy/oldwang.sh

-r-xr--r-- 1 oldboy oldboy 4 Nov  3 18:34 /oldboy/oldwang.sh

\[oldboy@oldboyedu42-lnb oldboy\]$

下面为何报错的原因是什么？

\[oldboy@oldboyedu42-lnb oldboy\]$ echo '\#' &gt;&gt; /etc/hosts

-bash: /etc/hosts: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ echo '\#' &gt;&gt; /etc/hosts

-bash: /etc/hosts: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -l /etc/hosts

-rw-r--r--. 2 root root 194 Nov 11  2017 /etc/hosts

\[oldboy@oldboyedu42-lnb oldboy\]$ \#oldboy用户

\[oldboy@oldboyedu42-lnb oldboy\]$ \#oldboy用户与这个文件关系: 陌生人

\[oldboy@oldboyedu42-lnb oldboy\]$ id oldboy

uid=500\(oldboy\) gid=500\(oldboy\) groups=500\(oldboy\)

\[oldboy@oldboyedu42-lnb oldboy\]$

\[oldboy@oldboyedu42-lnb oldboy\]$ \#oldboy用户对这个文件权限 最后三位 r--

\[oldboy@oldboyedu42-lnb oldboy\]$ cat  /etc/shadow

cat: /etc/shadow: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ cat /etc/sudoers

cat: /etc/sudoers: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ ll /etc/sudoers

-r--r-----. 1 root root 3729 Dec  8  2015 /etc/sudoers

\#1.oldboy

\#2.oldboy 陌生人

\#3.最后三位 ---

#### 5、文件的读写执行小结\(限制普通用户\)：

1.r查看文件的内容

2.w修改文件的内容，需要r的配合

如果没有r权限，使用vi/vim 修改文件内容 会导致源文件内容清空

3.x执行文件（命令或脚本），需要r的配合

#### 练习题：

详细说出rwx在文件中的意义

