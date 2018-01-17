awk编程思想

1、awk核心思想就是先处理，然后END模块输出 （ 累加（a++;a+=$0）,awk数组 ）

2、BEGIN模块用于awk内置变量 FS, RS的赋值，打印标题头信息 （excel表格里面标题行）

要在awk执行前，定义好

3、END模块用来最后输出，统计信息，awk数组信息 （累加（a++;a+=$0） awk数组）

\[root@oldboy files\]\# cat awkfile.txt

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

\[root@oldboy files\]\# awk -F : 'BEGIN{print "user","UID"}{print $1,$3}' awkfile.txt \|column -t

user UID

root 0

bin 1

daemon 2

adm 3

lp 4

sync 5

shutdown 6

halt 7

mail 8

uucp 10

awk 'BEGIN{print "hello world!"}{print NR,$0}END{print "end of file"}' count.txt

hello world!

1 root x root root bin bash

2 bin x bin bin sbin nologin

3 daemon x daemon sbin sbin nologin

4 adm x adm var adm sbin nologin

5 lp x lp var spool lpd sbin nologin

6 sync x sync sbin bin sync

7 shutdown x shutdown sbin sbin shutdown

8 halt x halt sbin sbin halt

9 mail x mail var spool mail sbin nologin

10 uucp x uucp var spool uucp sbin nologin

end of file

统计/etc/services文件里面的空行数量

\[root@nfsserver files\]\# awk '$0~/^$/{a++}END{print a}' /etc/services

16

\[root@oldboy files\]\# grep -c "^$" /etc/services

16

企业面试题： awkfile2.txt里面以:为分隔符，区域3大于15，一共有多少行？

\[root@nfsserver files\]\# head -20 /etc/passwd &gt; awkfile2.txt

\[root@nfsserver files\]\# awk -F ":" '$3&gt;15{a+=1;print a}' awkfile2.txt

1

2

3

4

5

6

\[root@nfsserver files\]\# awk -F ":" '$3&gt;15{a+=1}END{print a}' awkfile2.txt

6

7.1 a++

a=a+1 ==&gt; a++

a=a+2 ==&gt; a+=2

a=a+$0 ==&gt; a+=$0

\[root@nfsserver files\]\# seq 100 \| awk '{a=a+$0}END{print "the result is:"a }'

the result is:5050

\[root@oldboy files\]\# seq 5

1

2

3

4

5

\[root@oldboy files\]\# seq 5 \|awk '{sum=sum+$0}END{print sum}'

15

7.2 企业案例

找出环境变量$PATH中，所有只有三个任意字符的命令，例如tee，并将他们重定向到

command.txt中，要求一行显示1个，并在文件尾部统计他们的个数

通配符：用来匹配文件名的 {}字符序列

正则表达：字符串

\[root@nfsserver ~\]\# find $\(echo $PATH \|tr ":" " "\) -type f -name "???" 2&gt;/dev/null \|awk '{a++}END{print a}'

69

