#### 1、变量

放东西  查看变量的内容

LANG----变量的名字----藏经阁里面的武功秘籍（葵花宝典）秘籍名字（书名）

$LANG----查看变量里面的内容----手端着书（葵花宝典）看书的内容（读书）

LANG=新的内容 ---向变量密码放入东西---修改书的内容（升级书）

欲练此功，必先自宫，若不自宫，也能成功



自定义的值，取一个名字去调用

alex=hello

echo $alex

#### 2、环境变量

linux哪里都可以用 大写 PS1 LANG PATH

\[root@oldboyedu44 ~\]\# \#env              ===&gt;查看系统中的环境变量

\[root@oldboyedu44 ~\]\# head -3 /etc/profile

\# /etc/profile



\# System wide environment and startup programs, for login setup

\[root@oldboyedu44 ~\]\# \#environment

#### 3、PATH环境变量作用

存放的是命令的路径

\[root@oldboyedu44 ~\]\# echo $PATH

/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin



