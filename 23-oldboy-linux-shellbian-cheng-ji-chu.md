### 第1章 shell 基础

#### 1.1 什么是shell

shell 是命令解释器，它在操作系统的最外层，负责直接与用户对话，把用户的输入解释给操作系统，并处理各种各样的操作系统的输出结果，输出屏幕返回给用户。

#### 1.1.1 交互方式

1）交互的方式：从键盘输入命令，通过/bin/bash 解析，可以立即得到shell的回应

2）非交互的方式：脚本

#### 1.1.2 Shell 执行命令分为两种方式：

1）内置命令：讲过的cd ，pwd， exit 和echo 等命令，当用户登陆系统后，shell 以及内置命令就会被系统载入到内存，并且一直运行。

2）一般命令：如ls, 磁盘上的程序文件——》调入内存——》执行命令

![](/assets/22-1.png)

### 1.2 什么是Shell脚本

当linux命令或语句不在命令行下执行（严格说，命令行也是shell）而是通过一个程序文件执行时，该程序就被称为Shell 脚本或shell 程序。

用户可以在shell 脚本中敲入一系列的命令及命令语句组合。这些命令，变量和流程控制语句等有机会的结合起来就形成一个功能强大的Shell脚本。

#### 注意事项：

1）有没有脚本放在统一的目录

2）权限：用哪个用户执行文件

3）清空文件怎么办，该怎么办

4）错误提示：有没有成功知不知道

5）脚本通用性

![](/assets/22-11.png)

### 1.3 shell脚本在运维工作中的作用地位

shell脚本擅长处理纯文本类型的数据，而linux中几乎所有配置文件、日志文件等都是纯文本类型文件。

### 第2章 shell脚本建立和执行

### 2.1 shell脚本的建立

使用vim 编辑器编辑脚本，可以事先做个别名

\[root@oldboyedu ~\]\# echo "alias vi= 'vim'" &gt;&gt;/etc/profile

\[root@oldboyedu ~\]\# . /etc/profile

#### 2.1.1 脚本开头（第一行）

规范的shell 脚本第一行会指出哪个程序（解释器），来执行脚本的内容，在linux bash编程中一般为：

\#!/bin/bash

或

\#!/bin/sh  &lt;&lt;===255字符以内

##### 其中开头的“\#！”又称为幻数，在执行shell 脚本中，内核会根据“\#！”后的解释器来确定用哪个程序解释脚本中的内容，注意：这一行必须在每个脚本顶端的第一行，如果不是第一行则为脚本注释行。

bash版本

\[root@oldboyedu ~\]\# bash --version

GNU bash, version 4.1.2\(1\)-release \(x86\_64-redhat-linux-gnu\)

Copyright \(C\) 2009 Free Software Foundation, Inc.

License GPLv3+: GNU GPL version 3 or later &lt;[http://gnu.org/licenses/gpl.html&gt;](http://gnu.org/licenses/gpl.html&gt);

This is free software; you are free to change and redistribute it.

There is NO WARRANTY, to the extent permitted by law.

\[root@oldboyedu ~\]\#

#### 2.1.2 shell 脚本的执行

shell脚本执行的四种方式：

1）bash script-name 或sh script-name

这种方法是当脚本本身没有可执行权限时常使用的方法

2\)path/script-name 或./script-name \(全路径或当前路径执行脚本\)

这种方法首选需要给脚本文件可执行权限

3）source script-name 或. script-name  \#注意“.” 点号，且点号后有空格。

source或.在执行这个脚本的同时，可以将脚本中的函数和变量加载到当前shell。不会产生子shell。又有点像nginx的include功能。

4）sh &lt;script -name 或cat script-name \|sh 或cat script -name\|bash

这种用法用的不多，我们在开机启动项优化使用过。

#### 

#### 2.1.3 shell脚本开发的规范和习惯

1）开头指定脚本解释器

2）开头加长版本版权等信息，可配置~/.vimrc 文件自动添加

3）脚本不要用中文注释，尽量用英文注释

4）脚本以.sh为扩展名。

5）放在统一的目录

6）代码书写优秀习惯

a: 成对的内容一次性写出来，防止遗漏，如；\[ \] , ‘’ ，“” 等

b:\[ \] 两端要有空格，先输入\[ \]，退格。输入2个空格，再退格写

c:流程控制语句一次书写完，再添加内容。heen

if 条件

then

内容

fi

```
   d通过缩进让代码易读

   f 脚本中引号都是英文状态下的引号，其他字符也是英文状态。
```

### 第3章 shell 环境变量

#### 3.1 变量类型

变量可分为2类

1）环境变量（也可以为全局变量）;可以在创建他们的shell及其生出来的子shell中使用，环境变量又可以分为自定义环境变量和bash内置的环境变量。

2）局部变量（普通变量）;只能在创建他们的shell函数或shell脚本中执行使用。

#### 3.2 环境变量

```
环境变量用于定义shell的运行环境，保证shell命令的正确执行，shell通过环境变量来确定登陆用户名、命令路径、终端类型、登陆目录等，所有的环境变量都是全局变量，可用于所有子进程中，包括编辑器、shell脚本和各类应用。但crond计划任务除外，还需要重新定义环境变量。
```

环境变量可以在命令行中设置，但用户退出这些变量志也会丢失，因此最好在用户家目录的.bash\_profile文件中或全局配置/etc/bashrc 、/etc/profile 文件或者/etc/profile.d 目录中定义。将环境变量放入profile 文件中，每次用户登陆这些变量值都将初始化。

通常，所有环境变量均为大写。环境变量应用于用户进程前，都因该用export命令导出。

##### 例如：export OLDBOY=1

### 第4章 shell局部（普通）变量

### 4.1 shell中变量名及变量内容的要求

```
一般是字母、数字、下划线组成。且以字母开头。如oldboy oldboy123 oldboy\_training .变量的内容，可以使用单引号或双引号引起来，或不加引号。

虽然变量可以下划线开头，但类似变量都是比较特殊的，都是系统自己用的，我们尽量少用。
```

\[root@oldboyedu ~\]\# \_123=eee

\[root@oldboyedu ~\]\# echo $\_123

eee

\[root@oldboyedu ~\]\# a=192.168.1.2

\[root@oldboyedu ~\]\# echo "a=$a"

a=192.168.1.2

\[root@oldboyedu ~\]\# b='192.168.1.2'

\[root@oldboyedu ~\]\# echo "b=$b"

b=192.168.1.2

\[root@oldboyedu ~\]\# c="192.168.1.2."

\[root@oldboyedu ~\]\# echo "c=${c}"

c=192.168.1.2.

### 4.2 变量名及变量内容定义小结

1）变量名只能由字母、数字。下划线组成，且以字母开头。

2）规范的变量名写法定义：见名知意。

a: OldboyAge=1 每个单词首字母大写

b: oldboy\_age=1 每个单词之间用“\_”

c:oldboyAgeSex=1 驼峰语法;首个单词字母小写，其余单词首字母大写。

3）=号的知识，a=1中的等号是赋值的意思，比较是不是相等于为“==”

4）打印变量，变量名前接$符号，变量名后接紧接字符时候，要用大括号括起来

5）注意变量内容引用方法，一般为双引号，简单连续字符可以不加引号，希望原样输出，使用单引号。

6）变量内容是命令，要用反引号\`\`或者$\(\)把变量括起来使用。

### 第5章 shell特殊变量

### 5.1 位置变量

##### 1）$0 获取当前执行的shell脚本的文件名，如果执行脚本带路径那么就包括脚本路径。

##### 2）$n 获取当前执行的shell脚本的第n个参数值，n=1..9, 当n为0时表示脚本的文件名，如果n大于9用括号括起来{10}{11}…… ,参数以空格隔开。

##### 3）$\#获取当前执行的shell脚本后面接参数的总个数。

\[root@oldboyedu scripts\]\# vim arg.sh

\#!/bin/bash

\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#

\# File Name: arg.sh

\# Version: V1.0

\# Author: oldboy

\# Organization: www.oldboyedu.com

\# Created Time : 2017-02-21 21:46:56

\# Description:

\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#

echo $0

echo $1 $2 $3 $4 $5 $6 $7 $8  $9 ${10} ${11} ${12} ${13}

echo $\#

arg.sh \[+\]                                                                                             10,8           All

"arg.sh" 22L, 301C written

\[root@oldboyedu scripts\]\# sh arg.sh

arg.sh

\[root@oldboyedu scripts\]\# sh /server/scripts/arg.sh

/server/scripts/arg.sh

\[root@oldboyedu scripts\]\# sh arg.sh 1 2 3 1 1 2 2 2 2 2 2 1 1 2 1 2 1

arg.sh

1 2 3 1 1 2 2 2 2 2 2 1 1

17

\[root@oldboyedu scripts\]\# sh arg.sh 1 2 3 1 1 2 2 2 2 2 2 1 1 2 1 2 1 3 8 9 8 6

arg.sh

1 2 3 1 1 2 2 2 2 2 2 1 1

22

##### 进程状态变量

##### 1）$? 获取执行上一个指令的返回值（0为成功，非0为失败）

测试

\[root@oldboyedu scripts\]\# cd /ddf

-bash: cd: /ddf: No such file or directory

\[root@oldboyedu scripts\]\# echo $?

1

\[root@oldboyedu scripts\]\# sh arg.sh

arg.sh

0

\[root@oldboyedu scripts\]\# echo $?

0

##### $?返回值参考

##### 0 表示运行成功

##### 2权限拒绝

##### 1-125表示运行失败，脚本命令、系统命令错误或参数传递错误。

##### 126 找到该命令，但无法执行

##### 127 未找到要运行的命令

##### &gt;128 命令被系统强制结束

### 第6章 变量的数值计算

### 6.1 \(\(\)\) 用法（常用于简单的整数运算）

算术运算符号

![](/assets/tab22-12.png)

##### 

##### 例子

\[root@oldboyedu scripts\]\# echo $\(\(1\*2+3/4-4\)\)

-2

\[root@oldboyedu scripts\]\# echo $\[1\*2+3/4-4\]

-2

\[root@oldboyedu scripts\]\# \(\(a=1+2\*3-4%3\)\)

\[root@oldboyedu scripts\]\# echo $a

6

\[root@oldboyedu scripts\]\# \(\(a=1+2\*\*3-4%3\)\)

\[root@oldboyedu scripts\]\# echo $a

8

\[root@oldboyedu scripts\]\# b=$\(\(1+2\*\*3-4%3\)\)

\[root@oldboyedu scripts\]\# echo $b

8

\[root@oldboyedu scripts\]\#

##### 小结：

##### 1：“\(\(\)\)” 在命令行执行时不需要$符号，但是输出需要$符号。

##### 2：“\(\(\)\)” 里所有字符之间有无或多个空格没有任何影响。

##### 3; \[ \]与\(\(\)\) 作用是一样的

### 第7章 脚本中定义变量

### 7.1 脚本中直接赋值

\[root@oldboyedu scripts\]\# vim arg.sh

\#!/bin/bash

a=6

b=2

echo "a-b =$\(\( $a - $b \)\)"

echo "a+b =$\(\( $a + $b \)\)"

echo "a\*b =$\(\( $a \* $b \)\)"

echo "a/b =$\(\( $a / $b \)\)"

echo "a\*\*b =$\(\( $a \*\* $b \)\)"

echo "a%b = $\(\( $a % $b \)\)"

\[root@oldboyedu scripts\]\# sh arg.sh

a-b =4

a+b =8

a\*b =12

a/b =3

a\*\*b =36

a%b = 0

### 7.2 命令行传参

```
利用位置变量
```

\[root@oldboyedu scripts\]\# vim arg.sh

\#!/bin/bash

##### a=$1   \#不需要把后面的$a、$b都改

b=$2

echo "a-b =$\(\( $a - $b \)\)"

echo "a+b =$\(\( $a + $b \)\)"

echo "a\*b =$\(\( $a \* $b \)\)"

echo "a/b =$\(\( $a / $b \)\)"

echo "a\*\*b =$\(\( $a \*\* $b \)\)"

echo "a%b = $\(\( $a % $b \)\)"

### 第8章 条件测试

```
什么是条件测试呢？

简单理解，判断某些条件是否成立，成立执行一种命令，不成立执行另一种命令。
```

### 8.1 条件测试语法

```
格式：\[ &lt;测试表达式&gt; \]  大家掌握这一种，其他的方法能看懂就即可。
```

### 8.2 测试表达式

##### 好习惯：先敲一对\[\]，然后退格输入2个空格\[  \]，最后再回退一个空格开始输入 \[ -f file \]

\[root@oldboyedu ~\]\# \[ -f /etc/hosts \] && echo 1 \|\| echo 0

1

\[root@oldboyedu ~\]\# \[ -f /etc/hosts1 \] && echo 1 \|\| echo 0

0

\[root@oldboyedu ~\]\# \[ ! -f /etc/hosts1 \] && echo 1 \|\| echo 0

1

##### \#在做测试判断时候，不一定用上面的方法，用下面的更简洁

\[root@oldboyedu ~\]\# \[ -f /etc/hosts \] && echo 1

1

\[root@oldboyedu ~\]\# \[ -f /etc/hosts1 \] \|\| echo 0

0

\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#

\[root@oldboyedu scripts\]\# \[ -f /etc/hosts \] && echo true \|\| echo false

true

\[root@oldboyedu scripts\]\# \[ -f /etc/host \] && echo true \|\| echo false

false

\[root@oldboyedu scripts\]\# \[ -f /date  \] && echo true \|\| echo false

false

\[root@oldboyedu scripts\]\# \[ -d /data  \] && echo true \|\| echo false

true

### 8.3 常用文件测试操作符号

![](/assets/tab22-13.png)

### 8.4 字符串测试操作符号

字符串测试操作符的作用：比较两个字符串是否相同、字符串长度度是否为零，字符串是否为NULL。。bash 区分零长度字符串和空字符串。

![](/assets/tab22-14.png)

#### 8.4.1 例子

\[root@oldboyedu ~\]\# \[ "a" = "b" \] && echo True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ "ab" = "ab" \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[  $x = $y \] && echo True \|\| echo False

False

\[root@oldboyedu ~\]\# \[  $x != $y \] && echo True \|\| echo False

True

系统脚本：

\[root@oldboyedu ~\]\# sed -n '30,31p' /etc/init.d/network

\# Check that networking is up.

\[ "${NETWORKING}" = "no" \] && exit 6

### 8.5 整数二元比较操作符

![](/assets/tab22-15.png)

### 8.6 逻辑操作符

![](/assets/tab22-16.png)

小结：

1）多个\[ \] 之间的逻辑操作符是 &&或\| \|

2）&& 前面成功执行后面

3）\|\|前面不成功执行后面

##### 例子

\[root@oldboyedu ~\]\# \[ 1 = 1  -a 2 -lt 3 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 = 1 -a 2 -lt 1 \] && echco True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ 1 = 1 -o 2 -lt 1 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 != 1 -o 2 -lt 1 \] && echo Rrue \|\| echo False

False

\[root@oldboyedu ~\]\#

小结：

与  所有子表达式都成立，总表达式才成立

或  只要有一个子表达式成立，那么总表达式就会成立。只有当所有子表达式不成立，总表达式才会不成立。

非  取反

### 第9章 条件测试

#### 9.1 条件测试语法

#### 9.2 \[ 测试表达式 \]

#### 9.3 常用文件测试操作符号

### 第10章 if条件语句

### 10.1 if单分支条件语句

if \[ 条件 \]

then

```
指令
```

fi

或者

if \[ 条件 \];then

指令

fi

提示：分号相当于命令换行，上面两种语句等同。

特殊写法if \[ -f "$file1" \];then echo 1;fi 相当于 \[ -f "$file1" \] && echo 1

#### 10.1.1

![](/assets/22-18.png)

\[root@oldboyedu scripts\]\# cat compare.sh

\#!/bin/bash

read -p "Please enter two num: " x y

\#No1 判断是否输入两个数字

\[ -z "$x" -o -z "$y" \] &&\

echo "Please enter the first num." &&\

exit 1

\#No2 判断是否是数字

\[ -z "\`echo $x\|sed 's\#\[0-9\]\#\#g'\`" -a -z "\`echo $y\|sed 's\#\[0-9\]\#\#g'\`" \] \|\|\

```
{

echo "ERROR: Maybe one of your input is not int!"

exit 2
```

}

\#No3 比较数值大小

if \[ $x -gt $y \]

then

```
echo "$x &gt; $y"

exit
```

fi

if \[ $x -eq $y \]

then

```
echo "$x = $y"

exit
```

fi

if \[ $x -lt $y \]

then

```
echo "$x &lt; $y"

exit
```

fi

### 10.2 if双分支条件语句

![](/assets/22-19.png)

\[root@oldboyedu scripts\]\# cat compare.sh

\#!/bin/bash

read -p "Please enter two num: " x y

\#No1 判断是否输入两个数字

\[ -z "$x" -o -z "$y" \] &&\

echo "Please enter the first num." &&\

exit 1

\#No2 判断是否是数字

```
{

echo "ERROR: Maybe one of your input is not int!"

exit 2
```

}

\#No3 比较数值大小

if \[ $x -gt $y \]

then

```
echo "$x &gt; $y"

\#exit
```

else

```
if \[ $x -eq $y \]

then

    echo "$x = $y"

    \#exit

else

    echo "$x &lt; $y"

fi
```

fi

### 10.3 多分支if语句

语法：

![](/assets/22-20.png)

\[root@oldboyedu scripts\]\# cat compare.sh

\#!/bin/bash

read -p "Please enter two num: " x y

\#No1 判断是否输入两个数字

\[ -z "$x" -o -z "$y" \] &&\

echo "Please enter the first num." &&\

exit 1

\#No2 判断是否是数字

```
{

echo "ERROR: Maybe one of your input is not int!"

exit 2
```

}

\#No3 比较数值大小

if \[ $x -gt $y \]

then

```
echo "$x &gt; $y"
```

elif \[ $x -eq $y \]

then

```
echo "$x = $y"
```

else

```
echo "$x &lt; $y"
```

fi

### 第11章 case结构条件语句

### 11.1 case结构条件句语法

![](/assets/22-21.png)

![](/assets/22-22.png)

### 11.2 给指定文本加颜色

echo -e "\033\[30m 黑色字oldboy trainning \033\[0m"

echo -e "\033\[31m 红色字oldboy trainning \033\[0m"

echo -e "\033\[32m 绿色字oldboy trainning \033\[0m"

echo -e "\033\[33m 黄色字oldboy trainning \033\[0m"

echo -e "\033\[34m 蓝色字oldboy trainning \033\[0m"

echo -e "\033\[35m 紫色字oldboy trainning \033\[0m"

echo -e "\033\[36m 天蓝字oldboy trainning \033\[0m"

echo -e "\033\[37m 白色字oldboy trainning \033\[0m"

### 11.3 echo给字符串加不同颜色

#### 11.3.1 直接加颜色

echo -e "\033\[40;37m 黑底白字 welcome to old1boy\033\[0m"

echo -e "\033\[41;37m 红底白字 welcome to old2boy\033\[0m"

echo -e "\033\[42;37m 绿底白字 welcome to old3boy\033\[0m"

echo -e "\033\[43;37m 黄底白字 welcome to old4boy\033\[0m"

echo -e "\033\[44;37m 蓝底白字 welcome to old5boy\033\[0m"

echo -e "\033\[45;37m 紫底白字 welcome to old6boy\033\[0m"

echo -e "\033\[46;37m 天蓝白字 welcome to old7boy\033\[0m"

echo -e "\033\[47;30m 白底黑字 welcome to old8boy\033\[0m"

### 第12章 循环语句（while/for）

### 12.1 循环语句语法

#### 12.1.1 while条件句

![](/assets/22-23.png)

#### 12.1.2 for循环结构语法

### 12.2 while语句

#### 12.2.1 守护进程

#### 12.2.2 从1加到100

![](/assets/22-24.png)

#### 12.2.3 倒计时

### 12.3 防止脚本执行终端的方法

![](/assets/22-28.png)

12.4 for循环语句

12.4.1 打印列表元素

12.4.2 开机自启动项优化

12.4.3 在/oldboy目录批量创建文件

12.4.4 批量改名

12.4.5 批量创建用户并设置随机密码

12.4.6 获取当前目录下的目录名作为变量列表打印

12.4.7 九九乘法表

12.5 各种语法小结

12.6 获取随机数的集中方法

12.6.1 通过系统环境变量$RANDOM

12.6.2 通过openssl产生

12.6.3 通过时间获得随机数

12.6.4 urandom

12.6.5 UUID

12.7 break continue exit return

12.7.1 break continue exit对比

12.8 break

12.9 continue

第13章 shell脚本的调试

案例：将windows的文件系统格式转化为unix文件系统

\[root@oldboy34-niubility scripts\]\# dos2unix  new.sh

dos2unix: converting file new.sh to UNIX format ...

\[root@oldboy34-niubility scripts\]\# cat -A new.sh

\#!/bin/bash$

for i in \`seq 5\`$

do$

if \[ $i -eq 3 \] ;then$

```
exit;                                                                                                                $
```

fi$

echo $i$

done$

echo "ok"$

