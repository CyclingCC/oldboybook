在深入了解awk前，我们需要知道awk如何处理文件的。

#### 1、文件的创建

```
[root@oldboy ~]# mkdir /server/files/ -p
[root@oldboy ~]# head /etc/passwd > /server/files/awkfile.txt
[root@oldboy ~]# cat /server/files/awkfile.txt 
root:x:0:0:root:/root:/bin/bash
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

这个文件仅包含十行文件，我们使用下面的命令：

#### 2、awk执行过程演示

```
[root@oldboy ~]# awk 'NR>=2{print $0}' /server/files/awkfile.txt 
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

命令说明：

条件NR&gt;=2,表示行号大于等于2时候，执行{print $0}显示整行。

awk是通过一行一行的处理文件，这条命令中包含模式部分（条件）和动作部分（动作），awk将处理模式（条件）指定的行

#### 3、小结awk执行过程

1）awk读入第一行内容

2）判断是否符合模式中的条件NR&gt;=2

a，如果匹配则执行对应的动作{print $0}

b，如果不匹配条件，继续读取下一行

3）继续读取下一行

4）重复过程1-3，直到读取到最后一行（EOF：end of file）



