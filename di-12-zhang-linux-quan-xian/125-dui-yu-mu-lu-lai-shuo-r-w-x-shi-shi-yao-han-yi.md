#### 1、对于目录来说 rwx含义

\#r     read     查看目录里面的内容 ls 

\#w     write    可以在目录中 创建 删除  重命名文件

\#x     execute  是否可以进入\(cd\)目录中

#### 2、测试环境

mkdir -p /oldboy/test 

chown oldboy.oldboy  /oldboy/test

touch  /oldboy/test/stu{01..5}.txt 

#### 3、目录的R权限

\#\#root     目录r权限

\[root@oldboyedu42-lnb oldboy\]\# ll -d test

drwxr-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\[root@oldboyedu42-lnb oldboy\]\# chmod u=r test

\[root@oldboyedu42-lnb oldboy\]\# ll -d test

dr--r-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\#\#oldboy     目录r权限

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -ld test

dr--r-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\[oldboy@oldboyedu42-lnb oldboy\]$ ls test

ls: cannot access test/stu01.txt: Permission denied

ls: cannot access test/del.log: Permission denied

ls: cannot access test/stu02.txt: Permission denied

ls: cannot access test/stu03.txt: Permission denied

ls: cannot access test/stu04.txt: Permission denied

ls: cannot access test/stu05.txt: Permission denied

ls: cannot access test/del.sh: Permission denied

del.log  del.sh  stu01.txt  stu02.txt  stu03.txt  stu04.txt  stu05.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -l test

ls: cannot access test/stu01.txt: Permission denied

ls: cannot access test/del.log: Permission denied

ls: cannot access test/stu02.txt: Permission denied

ls: cannot access test/stu03.txt: Permission denied

ls: cannot access test/stu04.txt: Permission denied

ls: cannot access test/stu05.txt: Permission denied

ls: cannot access test/del.sh: Permission denied

total 0

-????????? ? ? ? ?            ? del.log

-????????? ? ? ? ?            ? del.sh

-????????? ? ? ? ?            ? stu01.txt

-????????? ? ? ? ?            ? stu02.txt

-????????? ? ? ? ?            ? stu03.txt

-????????? ? ? ? ?            ? stu04.txt

-????????? ? ? ? ?            ? stu05.txt

#### 4、目录的RX权限

##### \#\#root     目录rx权限

\[root@oldboyedu42-lnb oldboy\]\# chmod u=rx test

\[root@oldboyedu42-lnb oldboy\]\# ll -d test

dr-xr-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

##### \#\#oldboy查看 

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -ld test

dr-xr-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -l test

total 8

-rw-r--r--  1 root root 7 Oct 24 13:46 del.log

-rw-r--r--. 1 root root 7 Oct 24 08:52 del.sh

-rw-r--r--  1 root root 0 Nov  3 19:16 stu01.txt

-rw-r--r--  1 root root 0 Nov  3 19:16 stu02.txt

-rw-r--r--  1 root root 0 Nov  3 19:16 stu03.txt

-rw-r--r--  1 root root 0 Nov  3 19:16 stu04.txt

-rw-r--r--  1 root root 0 Nov  3 19:16 stu05.txt

##### 小结：

1.目录的r权限，查看目录里面内容 

2.目录来说r权限 需要有x配合 

3.对于目录来说x权限，cd   你是否能查看或修改目录里面文件属性

#### 5、目录的W权限

##### \#\#root     目录w权限

\[root@oldboyedu42-lnb oldboy\]\# chmod u=w test

\[root@oldboyedu42-lnb oldboy\]\# ll -d test

d-w-r-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

##### \#\#oldboy     目录w权限

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -ld test

d-w-r-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\[oldboy@oldboyedu42-lnb oldboy\]$ touch test/oldboy.txt

touch: cannot touch \`test/oldboy.txt': Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ rm -f test/stu01.txt

command bny -f test/stu01.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ \rm -f test/stu01.txt

rm: cannot remove \`test/stu01.txt': Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ \rm -f test/stu01.txt

rm: cannot remove \`test/stu01.txt': Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ \rm -f test/stu01.txt

rm: cannot remove \`test/stu01.txt': Permission denied

#### 6、目录的WX权限

##### \#\#root     目录wx权限

\[root@oldboyedu42-lnb oldboy\]\# chmod u=wx test

\[root@oldboyedu42-lnb oldboy\]\# ll -d test

d-wxr-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

##### \#\#oldboy     目录wx权限

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -ld test

d-wxr-xr-x. 2 oldboy oldboy 4096 Nov  3 19:16 test

\[oldboy@oldboyedu42-lnb oldboy\]$ touch test/oldboy.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ touch test/oldboy.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ ls test

ls: cannot open directory test: Permission denied

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -l test/oldboy.txt

-rw-rw-r-- 1 oldboy oldboy 0 Nov  3 19:30 test/oldboy.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ ls -l test/oldboy.tx

ls: cannot access test/oldboy.tx: No such file or directory

\[oldboy@oldboyedu42-lnb oldboy\]$ \rm -f test/stu01.txt

\[oldboy@oldboyedu42-lnb oldboy\]$ \rm -f test/stu01.txt

##### 小结

目录的w权限：

1.w权限表示 可以在目录中 创建 删除 重命名文件

2.w权限需要x权限配合

\[root@oldboyedu42-lnb ~\]\# cd /etc/

\[root@oldboyedu42-lnb etc\]\# touch oldboy.txt

\[root@oldboyedu42-lnb etc\]\# chmod 777 oldboy.txt

\[oldboy@oldboyedu42-lnb etc\]$ \rm -f oldboy.txt 

rm: cannot remove \`oldboy.txt': Permission denied

#### 7、目录权限小结：

1.r  查看目录内容 ，需要x权限配合 

2.w  在目录里面创建 删除 重命名文件  ，需要x权限配合  

3.x  进入到目录     查看目录中文件的属性

