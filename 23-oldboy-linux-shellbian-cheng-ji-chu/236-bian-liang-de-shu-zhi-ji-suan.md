### 变量的数值计算 {#第6章-变量的数值计算}

### 6.1 \(\(\)\) 用法（常用于简单的整数运算） {#61--用法（常用于简单的整数运算）}

算术运算符号

![](https://www.luffycity.com/linux-book/assets/tab22-12.png)

##### 

##### 例子 {#例子}

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

##### 小结： {#小结：}

##### 1：“\(\(\)\)” 在命令行执行时不需要$符号，但是输出需要$符号。 {#1：-在命令行执行时不需要符号，但是输出需要符号。}

##### 2：“\(\(\)\)” 里所有字符之间有无或多个空格没有任何影响。 {#2：-里所有字符之间有无或多个空格没有任何影响。}

##### 3; \[ \]与\(\(\)\) 作用是一样的 {#3--与-作用是一样的}



