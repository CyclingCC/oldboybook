#### 1.1 权限位置说明

![](https://www.luffycity.com/linux-book/assets/18-7.png)

#### 1.2 权限设置

![](https://www.luffycity.com/linux-book/assets/18-8.png)![](https://www.luffycity.com/linux-book/assets/18-9.png)

#### 1.3 普通文件的读、写、执行权限

1、可读r：表示具有读取/阅读文件内容的权限

2、可写w：表示具有新增、修改文件内容的权限

1）如果没有r配合，那么vi编辑文件会提示无法编辑（但可强制编辑），echo可以重定向或追加

2）特别提示：删除文件（修改文件名等）的权限是受父目录的权限控制，和文件本身权限无关

3、可执行x：表示具有执行文件的权限

1）文件本身要能够执行

2）普通用户同时还需要具备r的权限才能执行

3）root只要有x的权限就能执行

#### 1.4 目录的读、写、执行权限

1、可读r：表示具有浏览目录下面文件及子目录的权限，即可以执行ls dir

1）如果没有x权限，则不能进到目录里，即无法执行cd  dir

2）如果没有x权限，ls列表时可以看到所有文件名，但是会提示无权访问目录下文件

3）如果ls -l列表，所有的属性会带有问号，也会提示无权访问目录下文件，但是可以看到所有            文件名

2、可写w：表示具有增加 、删除、或修改目录内文件名（一般指文件名）的权限（需要x权限配合）

3、可执行x：表示具有进入目录的权限 例如可以执行cd dir

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

#### 1.5 权限测试三步

\#第一步-看看你是谁？

\#第二步-你和这个文件的关系（用户？ 一个组？ 其他人？ ）

\#第三步-权限

#### 1.6 测试环境

\[root@oldboy oldboy\]\# groupadd incahome

\[root@oldboy oldboy\]\# usermod -g incahome oldboy

\[root@oldboy oldboy\]\# id oldboy

uid=500\(oldboy\) gid=501\(incahome\) 组=501\(incahome\)

\[root@oldboy oldboy\]\# useradd test

\[root@oldboy oldboy\]\# mkdir /oldboy -p

\[root@oldboy oldboy\]\# echo "echo oldboylinux" &gt;/oldboy/test.sh

\[root@oldboy oldboy\]\# chmod +x /oldboy/test.sh

\[root@oldboy oldboy\]\# cat /oldboy/test.sh

#### 企业面试题：请从linux文件系统的角度详细描述读取/oldboy/test.sh文件的过程。

\[root@oldboy oldboy\]\# chmod u=-,g=x,o=w test/oldboy.sh

\[root@oldboy oldboy\]\# ls -l test

总用量 0

------x-w- 1 root root 0 3月 21 02:06 gongli.txt

------x-w- 1 root root 0 3月 21 02:03 oldboy.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod u=-,g=x,o=w test/oldgirl.sh

\[root@oldboy oldboy\]\# ls -l test

总用量 0

------x-w- 1 root root 0 3月 21 02:06 gongli.txt

------x-w- 1 root root 0 3月 21 02:03 oldboy.sh

------x-w- 1 root root 0 3月 21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod g+w test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-----wx-w- 1 root root 0 3月 21 02:06 gongli.txt

------x-w- 1 root root 0 3月 21 02:03 oldboy.sh

------x-w- 1 root root 0 3月 21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod u=rx,g-w,o=rx test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-x--xr-x 1 root root 0 3月 21 02:06 gongli.txt

------x-w- 1 root root 0 3月 21 02:03 oldboy.sh

------x-w- 1 root root 0 3月 21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod a-x test/gongli.txt

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-----r-- 1 root root 0 3月 21 02:06 gongli.txt

------x-w- 1 root root 0 3月 21 02:03 oldboy.sh

------x-w- 1 root root 0 3月 21 02:03 oldgirl.sh

-rwxrwxrwx 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\# chmod -R a=rx test

\[root@oldboy oldboy\]\# ls -l test

总用量 0

-r-xr-xr-x 1 root root 0 3月 21 02:06 gongli.txt

-r-xr-xr-x 1 root root 0 3月 21 02:03 oldboy.sh

-r-xr-xr-x 1 root root 0 3月 21 02:03 oldgirl.sh

-r-xr-xr-x 1 root root 0 3月 21 02:03 test.sh

\[root@oldboy oldboy\]\#

#### 1.7 文件访问过程-详解

![](https://www.luffycity.com/linux-book/assets/18-2.png)

