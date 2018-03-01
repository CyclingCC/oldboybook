#### 1、数组结构

数组名\\[下标\\] =值

arrayname\[string\]=value

#### 2、awk一些实例

```
[root@nfsserver files]# awk 'BEGIN{man="woman";print man}'
woman
[root@nfsserver files]# awk 'BEGIN{man="woman woman2 woman3";print man}'
woman woman2 woman3
[root@nfsserver files]# awk 'BEGIN{kuang[1]="woman";kuang[2]="woman2";kuang[3]="woman3";print kuang[1],kuang[2],kuang[3]}'
woman woman2 woman3
[root@oldboy36 ~]# awk 'BEGIN{kuang[a]="woman";kuang[b]="woman2";kuang[c]="woman3";print a,kuang[a],b,kuang[b],c,kuang[c]}'
woman3 woman3 woman3
[root@oldboy36 ~]# awk 'BEGIN{kuang["a"]="woman";kuang["b"]="woman2";kuang["c"]="woman3";print a,kuang["a"],b,kuang["b"],c,kuang["c"]}'
woman woman2 woman3
```

#### 3、awk数组说明

1）shell与awk中变量默认值为空

2）kuang\[a\] kuang\[b\] kuang\[c\] 中的a、 b、c 被认为是变量，都没有赋值，默认为空

所以 kuang\[a\] kuang\[b\] kuang\[c\] 是同一个元素，最终结果相同

3）数组元素名为字符串时必须用"" kuang\["a"\] kuang\["b"\] kuang\["c"\]

4）awk数组中的元素不一定是连续的，这点不同于其他语言的数组

#### 4、awk BEGIN模块

BEGIN模块在awk读取文件之前就执行，一般用来定义我们的内置变量（FS,RS等）

可以输出表头（excel表格名称）

BEGIN模块可以做一些测试，如算术运算

\[root@oldboy files\]\# awk 'BEGIN{print 10/3}'

3.33333

#### 5、awk END模块

END在awk读取完所有文件的时候，再执行END模块，一般用来输出一个结果（累加，数组结果），

也可以是和BEGIN模块类似的结尾标识信息

注意 BEGIN或END模块只能有一个

模式{动作} 可以是多个

'NR==2{print $1}NR==5{print $0}'

awk -F ":" 'NR==1{print NR,$0}NR==2{print NR,$NF}' awkfile.txt

#### 6、awk编程思想

1）awk核心思想就是先处理，然后END模块输出 （ 累加（a++;a+=$0）,awk数组 ）

2）BEGIN模块用于awk内置变量 FS, RS的赋值，打印标题头信息 （excel表格里面标题行）

要在awk执行前，定义好

3）END模块用来最后输出，统计信息，awk数组信息 （累加（a++;a+=$0） awk数组）

##### 例子：

##### 环境准备

```
[root@oldboy files]# cat awkfile.txt
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

```
[root@oldboy files]# awk -F : 'BEGIN{print "user","UID"}{print $1,$3}' awkfile.txt |column -t
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
```

案例：统计/etc/services文件里面的空行数量

\[root@nfsserver files\]\# awk '$0~/^$/{a++}END{print a}' /etc/services

16

\[root@oldboy files\]\# grep -c "^$" /etc/services

16

#### 企业面试题： awkfile2.txt里面以:为分隔符，区域3大于15，一共有多少行？

```
[root@nfsserver files]# head -20 /etc/passwd > awkfile2.txt
[root@nfsserver files]# awk -F ":" '$3>15{a+=1;print a}' awkfile2.txt
1
2
3
4
5
6
[root@nfsserver files]# awk -F ":" '$3>15{a+=1}END{print a}' awkfile2.txt
6
7.1 a++
a=a+1 ==> a++
a=a+2 ==> a+=2
a=a+$0 ==> a+=$0
[root@nfsserver files]# seq 100 | awk '{a=a+$0}END{print "the result is:"a }'
the result is:5050
[root@oldboy files]# seq 5
1
2
3
4
5
[root@oldboy files]# seq 5 |awk '{sum=sum+$0}END{print sum}'
15
```

#### 企业案例：找出环境变量$PATH中，所有只有三个任意字符的命令，例如tee，并将他们重定向到command.txt中，要求一行显示1个，并在文件尾部统计他们的个数

通配符：用来匹配文件名的 {}字符序列

正则表达：字符串

```
[root@nfsserver ~]# find $(echo $PATH |tr ":" " ") -type f -name "???" 2>/dev/null |awk '{a++}END{print a}'
69
```



