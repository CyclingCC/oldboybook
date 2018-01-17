-i 不区分大小写

-n 对匹配的内容显示行号

--color=auto

\[root@oldboy logs\]\# grep -n "." nginx.conf

1:stu01

2:stu02

3:stu03

4:stu04

5:stu05

6:stu06

7:stu07

8:stu08

9:stu09

10:stu10

11:stu11

12:stu12

13:stu13

14:stu14

15:stu15

16:stu16

17:stu17

18:stu18

19:stu19

20:stu20

\[root@oldgirl oldboy\]\# grep "oldboy" /etc/hosts

10.33.33.129 www.baidu.com oldboy

\[root@oldgirl oldboy\]\# grep --color=auto "oldboy" /etc/hosts

10.33.33.129 www.baidu.com oldboy

\[root@oldgirl oldboy\]\# echo "alias grep='grep --color=auto'" &gt;&gt;/etc/profile

\[root@oldgirl oldboy\]\# tail -1 /etc/profile

alias grep='grep --color=auto'

\[root@oldgirl oldboy\]\# . /etc/profile

welcome to oldboy linux training from /etc/profile.d

\[root@oldgirl oldboy\]\# grep --color=auto"oldboy" /etc/hosts

