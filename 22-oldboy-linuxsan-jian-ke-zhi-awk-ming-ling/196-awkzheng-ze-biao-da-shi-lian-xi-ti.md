练习题1:显示姓Zhang的人的第二次捐款金额及她的名字

练习题2:显示Xiaoyu的名字和ID号码

练习题3:显示所有以41开头的ID号码的人的全名和ID号码

练习题4:显示所有以一个D或X开头的人名全名

练习题5:显示所有ID号码最后一位数字是1或5的人的全名

练习题6:显示Xiaoyu的捐款，每个值都有以$开头。如$520$200$135

练习题7:显示所有人的全名，以姓，名的格式显示，如Meng，Feixue

**接下来我们通过练习题来联系awk如何使用正则表达式。**

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



