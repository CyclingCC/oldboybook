#### 1、单引号： 所见即所得，原封不动显示出来

\[root@oldboyedu42-lnb oldboy\]\# echo '$LANG $\(hostname\) \`whoami\` {1..5}'

$LANG $\(hostname\) \`whoami\` {1..5}

#### 2、双引号： 对特殊符号进行解析运行

\[root@oldboyedu42-lnb oldboy\]\# echo "$LANG $\(hostname\) \`whoami\` {1..5}"

en\_US.UTF-8 oldboyedu42-lnb root {1..5}

#### 3、不加引号：和双引号类似，支持通配符

\[root@oldboyedu42-lnb oldboy\]\# echo $LANG $\(hostname\) \`whoami\` {1..5}

en\_US.UTF-8 oldboyedu42-lnb root 1 2 3 4 5

#### 4、三者的区别

##### 引号和不加引号的区别1

\[root@oldboytx ~\]\# touch a b

\[root@oldboytx ~\]\# ll

total 0

-rw-r--r--. 1 root root 0 Jun 25 16:25 a

-rw-r--r--. 1 root root 0 Jun 25 16:25 b

\[root@oldboytx ~\]\# touch "a b"

\[root@oldboytx ~\]\# ll

total 0

-rw-r--r--. 1 root root 0 Jun 25 16:25 a

-rw-r--r--. 1 root root 0 Jun 25 16:25 a b

-rw-r--r--. 1 root root 0 Jun 25 16:25 b

##### 引号和不加引号的区别2

\[root@oldboy36 tmp\]\# ll

总用量 0

-rw-r--r-- 1 root root 0 6月 25 19:36 ?

-rw-r--r-- 1 root root 0 6月 25 19:32 \*

-rw-r--r-- 1 root root 0 6月 25 19:33 aa

-rw-r--r-- 1 root root 0 6月 25 19:33 abc

-rw-r--r-- 1 root root 0 6月 25 19:33 b

\[root@oldboy36 tmp\]\# ll ?

-rw-r--r-- 1 root root 0 6月 25 19:36 ?

-rw-r--r-- 1 root root 0 6月 25 19:32 \*

-rw-r--r-- 1 root root 0 6月 25 19:33 b

\[root@oldboy36 tmp\]\# ll "?"

-rw-r--r-- 1 root root 0 6月 25 19:36 ?

\[root@oldboy36 tmp\]\# ll \*

-rw-r--r-- 1 root root 0 6月 25 19:36 ?

-rw-r--r-- 1 root root 0 6月 25 19:32 \*

-rw-r--r-- 1 root root 0 6月 25 19:33 aa

-rw-r--r-- 1 root root 0 6月 25 19:33 abc

-rw-r--r-- 1 root root 0 6月 25 19:33 b

\[root@oldboy36 tmp\]\# ll "\*"

-rw-r--r-- 1 root root 0 6月 25 19:32 \*

##### 双引号和单引号区别1

关于$

\[root@oldboytx ~\]\# echo "$LANG"

en\_US.UTF-8

\[root@oldboytx ~\]\# echo '$LANG'

$LANG

##### 双引号和单引号区别2：

关于\`\`

\[root@oldboytx ~\]\# echo "\`which awk\`"

/bin/awk

\[root@oldboytx ~\]\# echo '\`which awk\`'

\`which awk\`

##### 双引号和单引号区别3：

##### 关于 !

\[root@oldboytx ~\]\# echo '!ll'

!ll

\[root@oldboytx ~\]\# echo "!ll"

echo "ll /bin/awk "

ll /bin/awk

\#通配符 {} \* \[\] ?

#### 练习题：

说一下单引号、双引号及不加引号的区别？

