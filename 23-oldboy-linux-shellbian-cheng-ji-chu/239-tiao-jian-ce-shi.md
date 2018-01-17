### if单分支条件语句 {#101-if单分支条件语句}

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

#### 10.1.1 {#1011}

![](https://www.luffycity.com/linux-book/assets/22-18.png)

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
echo "$x 
&
gt; $y"

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
echo "$x 
&
lt; $y"

exit

```

fi

### 10.2 if双分支条件语句 {#102-if双分支条件语句}

![](https://www.luffycity.com/linux-book/assets/22-19.png)

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
echo "$x 
&
gt; $y"

\#exit

```

else

```
if \[ $x -eq $y \]

then

    echo "$x = $y"

    \#exit

else

    echo "$x 
&
lt; $y"

fi

```

fi

### 10.3 多分支if语句 {#103-多分支if语句}

语法：

![](https://www.luffycity.com/linux-book/assets/22-20.png)

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

echo "$x 

&

gt; $y"



elif \[ $x -eq $y \]

then

echo "$x = $y"



else

```
echo "$x 
&
lt; $y"

```

fi

