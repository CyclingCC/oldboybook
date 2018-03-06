#### 1、添加一个用户mysql指定uid为888，禁止登陆并且不创建家目录。

#### 2、简述 raid0 raid1 raid5 raid10的工作原理和特点？

#### 3、列出/usr/目录下各个子目录占用的空间大小。

#### 4、填空题：12块2TB硬盘在不考虑HotSpare的情况下做RAID0,RAID1,RAID5后空间分别为（），（），（）。

#### 5、说出磁盘常见接口类型。

#### 6、sed命令练习题

```
[root@oldboyedu ~]# cat /tmp/passwd
root:x:0: 0:root:/root:/bin/bash

bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin
```

1\)删除每行开头的所有空格

2\)把所有小写字母用括号（）括起来

3\)删除文件中的所有空行

4\)删除头三行

5\)显示bin-halt开头之间的行

#### 7、Shell考试题

1\)CentOS默认的Shell是\_\_\_\_\_\_

2\)已知脚本如下所示

\# cat test.sh 

\#!/bin/bash

user=\`whoami\`

问sh test.sh后echo $user返回的结果  ?

3\)Shell变量分为	¬¬¬\_\_\_\_和\_\_\_\_和 \_\_\_\_

4\)说明下面变量的类型或作用

export OLDGIRL=oldboyedu      OLDGIRL是\_\_\_\_

password=123456              password是\_\_\_\_

$0 是	\_\_\_\_

$3 是	\_\_\_\_

$\# 是	\_\_\_\_

$? 是	\_\_\_\_

5\)找出下面有误的变量名

①x

②name

③passWord

④1jia

⑤123

⑥z\_123

错误的：

6\)写出2个环境变量配置文件和1个目录

①	\_\_\_\_

②	\_\_\_\_

③	\_\_\_\_

7\)根据题意写出对应脚本。

①判断/data目录是否存在，存在则进入目录并查看文件属性。

②判断/etc/hosts文件是否存在，存在则将文件复制到/tmp目录下。

