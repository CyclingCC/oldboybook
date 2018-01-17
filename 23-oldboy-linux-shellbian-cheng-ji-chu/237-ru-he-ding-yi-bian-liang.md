### 脚本中直接赋值 {#71-脚本中直接赋值}

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

### 7.2 命令行传参 {#72-命令行传参}

```
利用位置变量
```

\[root@oldboyedu scripts\]\# vim arg.sh

\#!/bin/bash

##### a=$1 \#不需要把后面的$a、$b都改 {#a1---不需要把后面的a、b都改}

b=$2

echo "a-b =$\(\( $a - $b \)\)"

echo "a+b =$\(\( $a + $b \)\)"

echo "a\*b =$\(\( $a \* $b \)\)"

echo "a/b =$\(\( $a / $b \)\)"

echo "a\*\*b =$\(\( $a \*\* $b \)\)"

echo "a%b = $\(\( $a % $b \)\)"

###  {#第8章-条件测试}



