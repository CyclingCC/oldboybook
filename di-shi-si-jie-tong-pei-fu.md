第1章 通配符

用于匹配文件名

 \[root@oldboy test\]\# ls

gongli  oldboy.sh  oldgilr.sh  test.sh

\[root@oldboy test\]\# ls \*.sh

oldboy.sh  oldgilr.sh  test.sh



1.1 常见特殊符号

符号	含义

;	命令分隔符

\#	配置文件注释；  root用户命令终端提示符

~	家目录  cd ~

-	上一次所在路径 cd -

su -    linux切换用户环境

^	非  \[^abcd\]

$	变量前加$ 取出变量内容

''	原样输出

""	$  \`\`  !  这几个符号可以解析，其它的字符原样输出

!	非，取反  \[!abcd\]

!命令  执行之前执行过的命令

!+数字   执行history中对应数字的命令

\`\`	用来引用命令    相当于$\(\)

{}	内容序列  

   {a,c,h}   表示  a  c  h

   {a..z}    表示  a 到  z

命令区块组合（模块）

linux正则中，表示重复次数  {3,5}  表示 3到5次

\(\)	字符序列分组

\|\|	或  前面命令执行失败的，才执行后面的命令

\|	管道 ； 或

&&	与    前面命令执行成功，才执行后面的命令

&	与  ； 命令后台运行

.	当前目录；linux中隐藏文件名的开头；正则表达式中的任意一个字符;加载一个文件内容

..	上级目录；{a..z}

/	根  或  路径分隔符

\	linux中放在命令关键字前面，用来屏蔽系统别名；转义

\*	代表任意多个任意字符；linux正则中，重复前面一个字符任意次

?	代表任意一个字符；linux正则中，重复前面一个字符0次或1次

+	重复前面一个字符1次或多次

\[\]	同样代表“一定有一个在括号内”的字符（非任意字符）。例如 \[abcd\] 代表“一定有一个字符， 可能是 a, b, c, d 这四个任何一个”

\[-\]	若有减号在中括号内时，代表“在编码顺序内的所有字符”。例如 \[0-9\] 代表 0 到 9 之间的所有数字，因为数字的语系编码是连续的！

\[^\]	若中括号内的第一个字符为指数符号 （^） ，那表示“反向选择”，例如 \[^abc\] 代表 一定有一个字符，只要是非 a, 非b, 非c 的其他字符就接受的意思。





\[root@oldboy test\]\# echo "$\(date\)"

2016年 03月 27日 星期日 15:56:11 CST





\[root@oldboy test\]\# cp /etc/sysconfig/network-scripts/ifcfg-eth0{,.bak} 

\[root@oldboy test\]\# ll /etc/sysconfig/network-scripts/ifcfg-eth0\*

-rw-r--r--. 3 root root 128 3月  20 08:55 /etc/sysconfig/network-scripts/ifcfg-eth0

-rw-r--r--  1 root root 128 3月  27 16:12 /etc/sysconfig/network-scripts/ifcfg-eth0.bak





\[root@oldboy test\]\# echo {1..5}

1 2 3 4 5

\[root@oldboy test\]\# seq -s " " 5

1 2 3 4 5



\[root@oldboy test\]\# mkdir {1..5}/{a..f} -p

\[root@oldboy test\]\# tree

.

├── 1

│   ├── a

│   ├── b

│   ├── c

│   ├── d

│   ├── e

│   └── f

├── 2

│   ├── a

│   ├── b

│   ├── c

│   ├── d

│   ├── e

│   └── f

├── 3

│   ├── a

│   ├── b

│   ├── c

│   ├── d

│   ├── e

│   └── f

├── 4

│   ├── a

│   ├── b

│   ├── c

│   ├── d

│   ├── e

│   └── f

├── 5

│   ├── a

│   ├── b

│   ├── c

│   ├── d

│   ├── e

│   └── f

├── gongli

├── oldboy.sh

├── oldboy.txt

├── oldgilr.sh

└── test.sh

1.2  shell中单引号、双引号及不加引号的区别

单引号： 所见即所得，单引号内的内容原样输出

双引号： 双引号内可以解析 \`\`  和 $  ,其它内容原样输出

无引号： 特殊符号有自己含义的都解析出来，数字、字母原样输出





深入浅出三剑客之awk必杀技一例

http://oldboy.blog.51cto.com/2561410/950730

深入浅出linux三剑客之sed必杀技一例

http://oldboy.blog.51cto.com/2561410/949365 

