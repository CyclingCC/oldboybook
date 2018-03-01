BEGIN模块再awk读取文件之前就执行，一般用来定义我们的内置变量（预定义变量，eg:FS，RS\),可以输出表头（类似excel表格名称）

BEGIN模式之前我们有在示例中提到，自定义变量，给内容变量赋值等，都使用过。需要注意的是BEGIN模式后面要接跟一个action操作块，包含在大括号内。awk必须在输入文件进行任何处理前先执行BEGIN里的动作（action）。我们可以不要任何输入文件，就可以对BEGIN模块进行测试，因为awk需要先执行完BEGIN模式，才对输入文件做处理。BEGIN模式常常被用来修改内置变量ORS，RS，FS，OFS等值。

#### 1、BEGIN模块

1）第一个作用，内置变量的定义

例1：取eth0的IP地址

```
[root@www files]# ifconfig eth0|awk -F "(addr:)|( Bcast:)" 'NR==2{print $2}'
192.168.197.133 
[root@www files]# ifconfig eth0 | awk -F "[ :]+" 'NR==2{print $4}'
192.168.197.133
[root@www files]# ifconfig eth0 | awk -F "[^0-9.]+" 'NR==2{print $2}'
192.168.197.133
```

\#上面的也可以写成

```
[root@www files]# ifconfig eth0 | awk 'BEGIN{FS="(addr:)|( Bcast:)"} NR==2{print $2}'
192.168.197.133 
[root@www files]# ifconfig eth0 | awk 'BEGIN{FS="[ :]+"}NR==2{print $4}'
192.168.197.133
[root@www files]# ifconfig eth0 | awk 'BEGIN{FS="[^0-9.]+"}NR==2{print $2}'
192.168.197.133
```

注意：

命令行-F本质就是修改的FS变量

2）第二个作用，在读取文件之前，输出些提示性信息（表头）。

```
[root@www files]# awk -F: 'BEGIN{print "username","UID"}{print $1,$3}' awkfile.txt 
username UID   #这就是输出的表头信息
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
```

说明：

要在第一行输出一些username和UID，我们应该想到BEGIN{}这个特殊的条件（模式），因为BEGIN{}在awk读取文件之前执行的。

所以结果是BEGIN{print "username","UID"},注意print命令里面双引号吃啥吐啥，原样输出。

然后我们实现了在输出文件内容之前输出“username”和“UID”，下一步输出文件的第一列和第三列即{print $1,$3}

最后结果就是BEGIN{print "username","UID"}{print $1,$3}

3）第三个作用，使用BEGIN模块的特殊性质，进行一些测试。

```
[root@www files]#简单输出内容：
[root@www files]# awk 'BEGIN{print "hello world!"}'
hello world!
[root@www files]# #进行计算
[root@www files]# awk 'BEGIN{print 10/3}'
3.33333
[root@www files]# awk 'BEGIN{print 10/3+1}'
4.33333
[root@www files]# awk 'BEGIN{print 10/3+1/4*9}'
5.58333
[root@www files]# #和变量有关的操作
[root@www files]# awk 'BEGIN{a=1;b=2;print a,b}'
1 2
[root@www files]# awk 'BEGIN{a=1;b=2;print a,b,a+b}'
1 2 3
```

4）第四种用法：配合getline读取文件，后面awk函数处讲解

#### 2、awk中变量的概念简介

直接定义，直接使用即可

awk中字母会被认为是变量，如果真的要给一个变量赋值字母（字符串），请使用双引号

```
[root@oldboy files]# awk 'BEGIN{a=abcd;print a}'
[root@oldboy files]# awk 'BEGIN{abcd=123456;a=abcd;print a}'
123456
[root@oldboy files]# awk 'BEGIN{a="abcd";print a}'
abcd
```

说明：

没有文件awk依旧可以处理BEGIN模式下的动作（命令）

#### 3、END模块

EHD在awk读取完所有的文件的时候，再执行END模块，一般用来输出一个结果（累加，数组结果），也可以是和BEGIN模块类似的结尾标识信息

```
[root@oldboy files]# awk 'BEGIN{print "hello world!"}{print NR,$0}END{print "end of file"}' count.txt 
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

与BEGIN模式相对应的END模式，格式一样，但是END模式仅在awk处理完所有输入行后才进行处理。

##### 企业案例：统计/etc/servies文件里的空行数量

思路：

a\)空行通过正则表达式来实现：^$

b\)统计数量：

grep -c

awk

方法一：grep

```
[root@oldboy files]# grep "^$" /etc/services | wc -l
16
[root@oldboy files]# grep -c "^$" /etc/services
16
```

说明：

grep命令-c表示count计数统计包含^$的行一共有多少。

方法二：

```
[root@oldboy files]# awk '/^$/{i++}END{print i}' /etc/services 
16
```

提示：

使用了awk的技术功能，很常用

第一步：统计空行个数

/^$/表示条件，匹配出空行，然后执行{i++}\(i++等于i=i+1\)即:/^$/{i=i+1}

我们可以通过/^$/{i=i+1;print i}来查看awk执行过程

```
[root@oldboy files]# awk '/^$/{i=i+1;print "the value of i is:"i}' /etc/services 
the value of i is:1
the value of i is:2
the value of i is:3
the value of i is:4
the value of i is:5
the value of i is:6
the value of i is:7
the value of i is:8
the value of i is:9
the value of i is:10
the value of i is:11
the value of i is:12
the value of i is:13
the value of i is:14
the value of i is:15
the value of i is:16
```

第二步：输出最后结果

但是我们只想要最后的结果16，不想要过程怎么办？使用END模式输出结果

因为END模式的特殊性质所以很适合输出最终结果

所以最终结果就是awk '/^$/{i=i+1}END{print "blank lines count:"i}' /etc/services

##### awk编程思想：

先处理，最后再END模块输出

{print NR,$0}body模块处理，处理完毕后

END{print "end of file"}输出一个结果

##### 企业面试题：文件count.txt,文件内容是1到100（由seq 100生成），请计算文件每行值加起来的结果（计算1+...+100）

思路：

文件每一行都有且只有一个数字，所以我们要让文件的每行内容相加。

回顾一下上一道题我们用的是i++即i=i+1

这里我们需要使用到第二个常用的表达式

i=i+$0

对比一下，其实只是把上边的1换成了$0

\[root@oldboy files\]\# awk '{i=i+$0}END{print i}' count.txt 

5050

