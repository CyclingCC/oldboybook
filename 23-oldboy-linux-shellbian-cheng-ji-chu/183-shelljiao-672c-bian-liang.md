### 一、shell环境变量

#### 1、变量类型 {#31-变量类型}

##### 变量可分为2类

1）环境变量（也可以为全局变量）;可以在创建他们的shell及其生出来的子shell中使用，环境变量又可以分为自定义环境变量和bash内置的环境变量。

2）局部变量（普通变量）;只能在创建他们的shell函数或shell脚本中执行使用。

##### 环境变量

环境变量用于定义shell的运行环境，保证shell命令的正确执行，shell通过环境变量来确定登陆用户名、命令路径、终端类型、登陆目录等，所有的环境变量都是全局变量，可用于所有子进程中，包括编辑器、shell脚本和各类应用。但crond计划任务除外，还需要重新定义环境变量。

环境变量可以在命令行中设置，但用户退出这些变量志也会丢失，因此最好在用户家目录的.bash\_profile文件中或全局配置/etc/bashrc 、/etc/profile 文件或者/etc/profile.d 目录中定义。将环境变量放入profile 文件中，每次用户登陆这些变量值都将初始化。

通常，所有环境变量均为大写。环境变量应用于用户进程前，都因该用export命令导出。

##### 例如：export OLDBOY=1 {#例如：export-oldboy1}

### 二、shell局部变量

#### 1、 shell中变量名及变量内容的要求

一般是字母、数字、下划线组成。且以字母开头。如oldboy oldboy123 oldboy\\_training .变量的内容，可以使用单引号或双引号引起来，或不加引号。

虽然变量可以下划线开头，但类似变量都是比较特殊的，都是系统自己用的，我们尽量少用。

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

#### 2、变量名及变量内容定义小结

1）变量名只能由字母、数字。下划线组成，且以字母开头。

2）规范的变量名写法定义：见名知意。

a: OldboyAge=1 每个单词首字母大写

b: oldboy\_age=1 每个单词之间用“\_”

c:oldboyAgeSex=1 驼峰语法;首个单词字母小写，其余单词首字母大写。

3）=号的知识，a=1中的等号是赋值的意思，比较是不是相等于为“==”

4）打印变量，变量名前接$符号，变量名后接紧接字符时候，要用大括号括起来

5）注意变量内容引用方法，一般为双引号，简单连续字符可以不加引号，希望原样输出，使用单引号。

6）变量内容是命令，要用反引号\`\`或者$\(\)把变量括起来使用。

### 三、特殊变量

#### 1、位置变量

1）$0 获取当前执行的shell脚本的文件名，如果执行脚本带路径那么就包括脚本路径。

2）$n 获取当前执行的shell脚本的第n个参数值，n=1..9, 当n为0时表示脚本的文件名，如果n大于9用括号括起来{10}{11}…… ,参数以空格隔开。

3）$\#获取当前执行的shell脚本后面接参数的总个数。

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

echo $1 $2 $3 $4 $5 $6 $7 $8 $9 ${10} ${11} ${12} ${13}

echo $\#

arg.sh \[+\] 10,8 All

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

#### 2、进程状态变量

$? 获取执行上一个指令的返回值（0为成功，非0为失败）

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

##### 小结：

$?返回值参考

0 表示运行成功

2权限拒绝

1-125表示运行失败，脚本命令、系统命令错误或参数传递错误。

126 找到该命令，但无法执行

127 未找到要运行的命令

&gt;128 命令被系统强制结束



### 四、变量的数值计算

### 五、如何定义变量



