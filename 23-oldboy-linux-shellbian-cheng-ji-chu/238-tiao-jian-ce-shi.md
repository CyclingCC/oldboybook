什么是条件测试呢？

简单理解，判断某些条件是否成立，成立执行一种命令，不成立执行另一种命令。

### 条件测试语法 {#81-条件测试语法}

```
格式：\[ 
&
lt;测试表达式
&
gt; \]  大家掌握这一种，其他的方法能看懂就即可。

```

### 8.2 测试表达式 {#82-测试表达式}

##### 好习惯：先敲一对\[\]，然后退格输入2个空格\[ \]，最后再回退一个空格开始输入 \[ -f file \] {#好习惯：先敲一对，然后退格输入2个空格--，最后再回退一个空格开始输入---f-file-}

\[root@oldboyedu ~\]\# \[ -f /etc/hosts \] && echo 1 \|\| echo 0

1

\[root@oldboyedu ~\]\# \[ -f /etc/hosts1 \] && echo 1 \|\| echo 0

0

\[root@oldboyedu ~\]\# \[ ! -f /etc/hosts1 \] && echo 1 \|\| echo 0

1

##### \#在做测试判断时候，不一定用上面的方法，用下面的更简洁 {#在做测试判断时候，不一定用上面的方法，用下面的更简洁}

\[root@oldboyedu ~\]\# \[ -f /etc/hosts \] && echo 1

1

\[root@oldboyedu ~\]\# \[ -f /etc/hosts1 \] \|\| echo 0

0

\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#

\[root@oldboyedu scripts\]\# \[ -f /etc/hosts \] && echo true \|\| echo false

true

\[root@oldboyedu scripts\]\# \[ -f /etc/host \] && echo true \|\| echo false

false

\[root@oldboyedu scripts\]\# \[ -f /date \] && echo true \|\| echo false

false

\[root@oldboyedu scripts\]\# \[ -d /data \] && echo true \|\| echo false

true

### 8.3 常用文件测试操作符号 {#83-常用文件测试操作符号}

![](https://www.luffycity.com/linux-book/assets/tab22-13.png)

### 8.4 字符串测试操作符号 {#84-字符串测试操作符号}

字符串测试操作符的作用：比较两个字符串是否相同、字符串长度度是否为零，字符串是否为NULL。。bash 区分零长度字符串和空字符串。

![](https://www.luffycity.com/linux-book/assets/tab22-14.png)

#### 8.4.1 例子 {#841-例子}

\[root@oldboyedu ~\]\# \[ "a" = "b" \] && echo True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ "ab" = "ab" \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ $x = $y \] && echo True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ $x != $y \] && echo True \|\| echo False

True

系统脚本：

\[root@oldboyedu ~\]\# sed -n '30,31p' /etc/init.d/network

\# Check that networking is up.

\[ "${NETWORKING}" = "no" \] && exit 6

### 8.5 整数二元比较操作符 {#85-整数二元比较操作符}

![](https://www.luffycity.com/linux-book/assets/tab22-15.png)

### 8.6 逻辑操作符 {#86-逻辑操作符}

![](https://www.luffycity.com/linux-book/assets/tab22-16.png)

小结：

1）多个\[ \] 之间的逻辑操作符是 &&或\| \|

2）&& 前面成功执行后面

3）\|\|前面不成功执行后面

##### 例子 {#例子}

\[root@oldboyedu ~\]\# \[ 1 = 1 -a 2 -lt 3 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 = 1 -a 2 -lt 1 \] && echco True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ 1 = 1 -o 2 -lt 1 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 != 1 -o 2 -lt 1 \] && echo Rrue \|\| echo False

False

\[root@oldboyedu ~\]\#

小结：

与 所有子表达式都成立，总表达式才成立

或 只要有一个子表达式成立，那么总表达式就会成立。只有当所有子表达式不成立，总表达式才会不成立。

非 取反

