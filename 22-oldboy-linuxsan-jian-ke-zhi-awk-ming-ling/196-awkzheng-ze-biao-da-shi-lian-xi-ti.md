练习题1:显示姓Zhang的人的第二次捐款金额及她的名字

练习题2:显示Xiaoyu的名字和ID号码

练习题3:显示所有以41开头的ID号码的人的全名和ID号码

练习题4:显示所有以一个D或X开头的人名全名

练习题5:显示所有ID号码最后一位数字是1或5的人的全名

练习题6:显示Xiaoyu的捐款，每个值都有以$开头。如$520$200$135

练习题7:显示所有人的全名，以姓，名的格式显示，如Meng，Feixue

#### 1、接下来我们通过练习题来联系awk如何使用正则表达式。

创建测试环境

```
[root@oldboy ~]# cat >>/server/files/reg.txt<<KOF
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
KOF
```

测试文件说明

```
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
```

说明：

* 第一列是姓氏
* 第二列是名字
* 第一列第二列合起来就是姓名
* 第三列是对应的ID号码
* 最后三列是三次捐款数量

1）显示姓Zhang的人的第二次捐款金额及她的名字

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$1~/^Zhang/{print $2,$(NF-1)}' reg.txt 
Zhang 100
Zhang 90
```

说明：

-F指定分隔符，现在大家知道了-F即FS也是支持正则表达式的。

【 ：】+ 表示连续的空格或冒号

-F “【 ：】+” 以连续的空格或冒号为分隔符

/Zhang/表示条件，整行中包含Dan字符的这个条件。

{print $1,$\(NF-1\)} 表示动作，满足条件后，执行显示第一列（$1）和倒数第二列（$\(NF-1\)）当然$5也可以。

注意：

NF是一行中有多少列，NF-1整行就是倒数第二列。

$\(NF-1\)就是取倒数第二列内容。

2）显示Xiaoyu的姓氏和ID号码

```
[root@oldboy files]#cat reg.txt  
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$2~/^Xiaoyu/{print $1,$3}' reg.txt 
Zhang 390320151
```

说明：

指定分隔符-F “【：】+”

$2~/Xiaoyu/表示条件，第二列包含Xiaoyu时候执行对应的动作

{print $1,$3}表示动作，显示第一列和第三列的内容

3）显示所有以41开头的ID号码的人的全名和ID号码

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$3~/^(41)/{print $1,$2,$3}' reg.txt 
Zhang Dandan 41117397
Liu Bingbing 41117483
```

4）显示所有以一个D或X开头的人名全名

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$2~/^D|^X/{print $1,$2}' reg.txt 
Zhang Dandan
Zhang Xiaoyu
Wang Xiaoai
```

说明：

-F “【 ：】+”指定分隔符

\|表示或，^以...开头

注意：

这里要用（）括号表示即^\(D\|X\)相当于^D\|^X，有的同学写成^D\|X这样是错误的。

5）显示所有ID号码最后一位数字是1或5的人的全名

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$3~/1$|5$/{print $1,$2}' reg.txt 
Zhang Xiaoyu
Wu Waiwai
Wang Xiaoai
Li Youjiu
Lao Nanhai
```

6）显示Xiaoyu的捐款，每个值都有以$开头。如$520$200$135

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ :]+" '$2~/Xiaoyu/{print "$"$4"$"$5"$"$6}' reg.txt 
$155$90$201
```

7）显示所有人的全名，以姓，名的格式显示，如Meng，Feixue

```
[root@oldboy files]# cat reg.txt 
Zhang Dandan    41117397    :250:100:175
Zhang Xiaoyu    390320151   :155:90:201
Meng  Feixue    80042789    :250:60:50
Wu    Waiwai    70271111    :250:80:75
Liu   Bingbing  41117483    :250:100:175
Wang  Xiaoai    3515064655  :50:95:135
Zi    Gege      1986787350  :250:168:200
Li    Youjiu    918391635   :175:75:300
Lao   Nanhai    918391635   :250:100:175
[root@oldboy files]# awk -F "[ ]+" '{print $1","$2}' reg.txt 
Zhang,Dandan
Zhang,Xiaoyu
Meng,Feixue
Wu,Waiwai
Liu,Bingbing
Wang,Xiaoai
Zi,Gege
Li,Youjiu
Lao,Nanhai
```

#### 2、企业面试题：取出网卡eth0的ip地址 {#企业面试题取出网卡eth0的ip地址}

最简单：hostname -I

**awk处理：**

方法一：

```
[root@oldboy files]# ifconfig eth0|awk 'BEGIN{RS="[ :]"}NR==31'
192.168.197.133
```

方法二：

```
[root@oldboy files]# ifconfig eth0 | awk -F "(addr:)|( Bcast:)" 'NR==2{print $2}'
192.168.197.133
```

方法三：

```
[root@oldboy files]# ifconfig eth0 | awk -F "[ :]+" 'NR==2{print $4}'
192.168.197.133
```

方法四：

```
[root@oldboy files]# ifconfig eth0 | awk -F "[^0-9.]+" 'NR==2{print $2}'
192.168.197.133
```

提示：

前边的三种方法都还是比较好理解的，这第四种方法，需要学会逆向思维，看看我们要的结果10.0.0.50，ip地址：数字和点（.），我是否可以指定分隔符，以数字和点以外的字符为分隔符呢？

换句话说就是要排除数字和点（.）正则表达式与排除常用的就是\[^0-9.\]即不匹配数字和点（.）

最后-F “\[^0-9\]”位分隔符，但是要使用+，表示连续的。合起来就是：awk -F “\[^0-9.\]+” 'NR==2{print $2}'

注意：

正则表达式是玩好awk的必要条件，必会掌握

#### 3、明明白白扩展正则表达式：+（加号）

```
[root@oldboy files]# echo "------======1########2"
------======1########2
[root@oldboy files]# echo "------======1########2" | grep "[-=#]"
------======1########2
[root@oldboy files]# echo "------======1########2" | grep -o "[-=#]"
-
-
-
-
-
-
=
=
=
=
=
=
#
#
#
#
#
#
#
#
```

#### 4、awk正则之{} -花括号

awk中的花括号有些不常用，但是偶尔会用到这里简单介绍。

1）取出awkfile中第一列包含一个o或者两个o的行

```
[root@oldboy files]# awk -F: '$1~/o{1,2}/' awkfile.txt 
[root@oldboy files]# awk -F: --posix '$1~/o{1,2}/' awkfile.txt 
root:x:0:0:root:/root:/bin/bash
daemon:x:2:2:daemon:/sbin:/sbin/nologin
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
[root@oldboy files]# awk -F: --re-interval '$1~/o{1,2}/' awkfile.txt 
root:x:0:0:root:/root:/bin/bash
daemon:x:2:2:daemon:/sbin:/sbin/nologin
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
```

#### 5、企业案例1:取出常用服务端口号

思路：

linux下面服务与端口信息的对应表格在/etc/services里面，所以这道题要处理/etc/services文件。

我们简单分析以下servics文件：

```
[root@oldboy ~]# sed -n '23,30p' /etc/services
tcpmux          1/tcp                           # TCP port service multiplexer
tcpmux          1/udp                           # TCP port service multiplexer
rje             5/tcp                           # Remote Job Entry
rje             5/udp                           # Remote Job Entry
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
```

从23行开始基本上每一行第一列是服务名称，第二列的第一部分是端口号，第二列的第二部分是tcp或udp协议。

方法：

```
[root@oldboy ~]# awk -F "[ /]+" '$1~/^(ssh)$|^(http)$|^(https)$|^(mysql)$|^(ftp)$/{print $1,$2}' /etc/services |sort|uniq
ftp 21
http 80
https 443
mysql 3306
ssh 22
```

提示：

\|是或者的意思，正则表达式

sort是将输出结果排序

uniq是去重复但不标记重复个数

uniq -c去重复但标记重复个数

#### 6、企业案例2:取出常用服务端名称

同学们自己尝试下

#### 7、比较表达式做为模式-需要一些例子

之前我们看了正则表达式在awk下的运用，下面再具体看看比较表达式如何在awk下工作。

awk是一种编程语言，能够进行更为复杂的判断，当条件为真时候，awk就执行相关的action。主要是针对某一区域做出相关的判断，比如打印成绩在80分以上的行，这样就必须对这一区域做比较判断，下表列出了awk可以使用的关系运算符，可以用来比较数字字符串，还有正则表达式。当表达式为真时候，表达式结果1，否0，只有表达式为真，awk才执行相关的action

![](/assets/21-15.png)

以上运算符是针对数字的，下面两个运算符之前已有示例，针对字符串

![](/assets/21-16.png)

##### 1）企业面试题：取出文件/etc/services的23～30行

**思路：**  
想表示一个范围，一个行的范围，就要用到NR这个内置变量了，同时也要用到比较表达式。

答案：

```
[root@www ~]# awk 'NR>=23&&NR<=30' /etc/services
[root@www ~]# awk 'NR>22&&NR<31' /etc/services
```

过程：

```
[root@www ~]# awk 'NR>=23&&NR<=30' /etc/services
tcpmux          1/tcp                           # TCP port service multiplexer
tcpmux          1/udp                           # TCP port service multiplexer
rje             5/tcp                           # Remote Job Entry
rje             5/udp                           # Remote Job Entry
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
[root@www ~]# awk 'NR>22&&NR<31' /etc/services
tcpmux          1/tcp                           # TCP port service multiplexer
tcpmux          1/udp                           # TCP port service multiplexer
rje             5/tcp                           # Remote Job Entry
rje             5/udp                           # Remote Job Entry
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
```

说明：

1）比较表达式比较常用的还是表示大于等于，小于等于或者等于，根据这个例子来学习即可

2）NR表示行号，大于等于23即，NR&gt;=23小于等于30，即NR&lt;=30

3\)合起来就是NR&gt;=23并且NR&lt;=30,&&表示并且，同时成立的意思。

4）换一种表达式方法就是大于22行小于31行，即NR&gt;22&&NR&lt;31

#### 8、如果判断某一列是否等于某个字符呢？

1）找出/etc/passwd中第五列是root的行

测试文件：

```
[root@www ~]# cat /server/files/awk_equal.txt
root:x:0:0:root:/root:/bin/bash
root:x:0:0:rootroot:/root:/bin/bash
root:x:0:0:rootrooot:/root:/bin/bash
root:x:0:0:rootrooot:/root:/bin/bash
root:x:0:0:/root:/bin/bash
```

答案：

```
awk -F":" '$5=="root"' /server/files/awk_equal.txt 
awk -F":" '$5~/^root$/' /server/files/awk_equal.txt
```

过程：

```
#方法一：
[root@www ~]# awk -F":" '$5=="root"' /server/files/awk_equal.txt 
root:x:0:0:root:/root:/bin/bash
#方法二：
[root@www ~]# awk -F":" '$5~/^root$/' /server/files/awk_equal.txt 
root:x:0:0:root:/root:/bin/bash
```

我们如果想要完全匹配root这个字符串，那就用$5=="root"即可，这也是答案里面给大家的。

```
#方法三：
此题也可通过正则匹配来限制root的字符串。$5~/^root$/
```

#### 练习题：

1、如果判断某一列是否等于某个字符呢？

2、取出文件/etc/services的15～20行



