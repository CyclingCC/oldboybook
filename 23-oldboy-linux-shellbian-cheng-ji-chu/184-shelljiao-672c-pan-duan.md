### 一、条件测试

##### 什么是条件测试呢？

简单理解，判断某些条件是否成立，成立执行一种命令，不成立执行另一种命令。

#### 1、条件测试语法

格式：\[ &lt;测试表达式&gt; \] 大家要掌握着一种，注意测试表达式两边要留空格

#### 2、测试表达式

好习惯：先敲一对\[\],然后退格输入2个空格\[\],最后再回退一个空格开始输入\[ -f file \]

\[root@chensiqi1 ~\]\# \[ -f /etc/hosts \] && echo 1 \|\| echo

1

\[root@chensiqi1 ~\]\# \[ -f /etc/hosts1 \] && echo 1 \|\| echo 0

0

\[root@chensiqi1 ~\]\# \[ ! -f /etc/hosts1 \] && echo 1 \|\| echo 0

1

\#在做测试判断时，不一定用上面的方法，用下面的写一半方法更简洁

\[root@chensiqi1 ~\]\# \[ -f /etc/hosts \] && echo 1

1

\[root@chensiqi1 ~\]\# \[ -f /etc/hosts1 \] \|\| echo 0

0

\#系统脚本

\[root@chensiqi1 ~\]\# vi /etc/init.d/nfs

....

\[ -x /usr/sbin/rpc.nfsd \] \|\| exit 5

\[ -x /usr/sbin/rpc.mountd \] \|\| exit 5

\[ -x /usr/sbin/exportfs \] \|\| exit 5

#### 3、常用文件测试操作符号

![](https://www.luffycity.com/linux-book/assets/tab22-13.png)

#### 4、字符串测试操作符号

字符串测试操作符的作用：比较两个字符串是否相同，字符串长度是否为零，字符串是否为NULL。Bash区分零长度字符串和空字符串。

\|常用字符串测试操作符\|说明\|

\|--\|--\|

\|-z "字符串"\|若串长度为0则真，-z理解为zero\|

\|-n “字符串”\|若串长度不为0则真，-n理解为no zero\|

\|“串1”=“串2”\|若串1等于串2则真，可以使用“==”代替“=”\|

\|“串1”!="串2"\|若串1不等于串2则真，但不能使用“!==”代替“!=”\|

特别注意，以上表格中的字符串测试操作符号务必要用“”引起来。\[ -z "$string"\]字符串比较，比较符号两端最好有空格，参考系统脚本。

\[ "$password" = "john" \]

提示：

\[,"password",=,"join",\]之间必须存在空格

\[root@chensiqi1 ~\]\# sed -n '30,31p' /etc/init.d/network

\# Check that networking is up.

\[ "${NETWORKING}" = "no" \] && exit 6

![](https://www.luffycity.com/linux-book/assets/tab22-14.png)

#### 5、 整数二元比较操作符

![](https://www.luffycity.com/linux-book/assets/tab22-15.png)

在\[\]中可以用&gt;和&lt;，但需要用\转义，虽然不报错，但结果不对。但还是不要混用！

#### 6、逻辑操作符

![](https://www.luffycity.com/linux-book/assets/tab22-16.png)

##### 小结

1）多个\[ \] 之间的逻辑操作符是 &&或\| \|

2）&& 前面成功执行后面

3）\|\|前面不成功执行后面

4）与 所有子表达式都成立，总表达式才成立

5）或 只要有一个子表达式成立，那么总表达式就会成立。只有当所有子表达式不成立，总表达式才会不成立。

6）非 取反

##### 例子 {#例子}

\[root@oldboyedu ~\]\# \[ 1 = 1 -a 2 -lt 3 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 = 1 -a 2 -lt 1 \] && echco True \|\| echo False

False

\[root@oldboyedu ~\]\# \[ 1 = 1 -o 2 -lt 1 \] && echo True \|\| echo False

True

\[root@oldboyedu ~\]\# \[ 1 != 1 -o 2 -lt 1 \] && echo Rrue \|\| echo False

False

#### 7、其他

##### 有的时候用\[\]比if要简单

\[ -f "$file" \] && echo 1 \|\| echo 0

if \[ -f "file" \];then echo 1;else echo 0;fi



