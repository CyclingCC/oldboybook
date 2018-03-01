1、基本的模式和动作

```
[root@oldboy ~]# awk -F ":" 'NR>=2 && NR<=6{print NR,$1}' /etc/passwd
2 bin
3 daemon
4 adm
5 lp
6 sync
```

命令说明：

-F 指定分隔符为冒号，相当于以“：”为菜刀，进行字段的切割。

NR&gt;=2 && NR&lt;=6：这部分表示模式，是一个条件，表示取第2行到第6行。

{print NR,$1}：这部分表示动作，表示要输出NR行号和$1第一列。

2、只有模式

```
[root@oldboy ~]# awk -F ":" 'NR>=2&&NR<=6' /etc/passwd
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
```

命令说明：

-F指定分隔符为冒号

NR&gt;=2&&NR&lt;=6这部分是条件，表示取第2行到第6行。

但是这里没有动作，这里大家需要了解如果只有条件（模式）没有动作，awk默认输出整行

3、只有动作

```
[root@oldboy ~]# awk -F ":" '{print NR,$1}' /etc/passwd
1 root
2 bin
3 daemon
4 adm
5 lp
6 sync
7 shutdown
8 halt
9 mail
10 uucp
以下省略....
```

命令说明：

-F指定分隔符为冒号

这里没有条件，表示对每一行都处理

{print NR,$1}表示动作，显示NR行号与$1第一列

这里要理解没有条件的时候，awk会处理每一行。

4、多个模式和动作

```
[root@oldboy ~]# awk -F ":" 'NR==1{print NR,$1}NR==2{print NR,$NF}' /etc/passwd
1 root
2 /sbin/nologin
```

命令说明：

-F指定分隔符为冒号

这里有多个条件与动作的组合

NR==1表示条件，行号（NR）等于1的条件满足的时候，执行{print NR,$1}动作，输出行号与第一列。

NR==2表示条件，行号（NR）等于2的条件满足的时候，执行{print NR,$NF}动作，输出行号与最后一列（$NF）

注意：

Pattern和{Action}需要用单引号引起来，防止shell作解释。

Pattern是可选的。如果不指定，awk将处理输入文件中的所有记录。如果指定一个模式，awk则只处理匹配指定的模式的记录。

{Action}为awk命令，可以是但个命令，也可以多个命令。整个Action（包括里面的所有命令）都必须放在{ 和 }之间。

Action必须被{ }包裹，没有被{ }包裹的就是Patern

file要处理的目标文件

1.6 awk执行过程

在深入了解awk前，我们需要知道awk如何处理文件的。



示例1-5 示例文件的创建



\[root@oldboy ~\]\# mkdir /server/files/ -p

\[root@oldboy ~\]\# head /etc/passwd &gt; /server/files/awkfile.txt

\[root@oldboy ~\]\# cat /server/files/awkfile.txt 

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

这个文件仅包含十行文件，我们使用下面的命令：



示例1-6 awk执行过程演示



\[root@oldboy ~\]\# awk 'NR&gt;=2{print $0}' /server/files/awkfile.txt 

bin:x:1:1:bin:/bin:/sbin/nologin

daemon:x:2:2:daemon:/sbin:/sbin/nologin

adm:x:3:4:adm:/var/adm:/sbin/nologin

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

sync:x:5:0:sync:/sbin:/bin/sync

shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown

halt:x:7:0:halt:/sbin:/sbin/halt

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin



命令说明：

条件NR&gt;=2,表示行号大于等于2时候，执行{print $0}显示整行。

awk是通过一行一行的处理文件，这条命令中包含模式部分（条件）和动作部分（动作），awk将处理模式（条件）指定的行



