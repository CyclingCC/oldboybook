### 一、特殊符号

#### 1、\#      注释   root用户的命令提示符

#### 2、$     取变量的内容\(命令行\)  取某一列\(awk\)  普通用户的命令提示符

#### 3、!     查找最近一次使用过的命令然后执行  find排除/取反 awk取反 vim强制

#### history \|grep awk

#### 4、\|     管道

#### ;     分割多条命令。

![](/assets/14-1.png)

![](/assets/14-2.png)

| \* | 代表任意多个任意字符；linux正则中，重复前面一个字符任意次 |
| :--- | :--- |
| ? | 代表任意一个字符；linux正则中，重复前面一个字符0次或1次 |
| + | 重复前面一个字符1次或多次 |
| \[\] | 同样代表“一定有一个在括号内”的字符（非任意字符）。例如 \[abcd\] 代表“一定有一个字符， 可能是 a, b, c, d 这四个任何一个” |
| \[-\] | 若有减号在中括号内时，代表“在编码顺序内的所有字符”。例如 \[0-9\] 代表 0 到 9 之间的所有数字，因为数字的语系编码是连续的！ |
| \[^\] | 若中括号内的第一个字符为指数符号 （^） ，那表示“反向选择”，例如 \[^abc\] 代表 一定有一个字符，只要是非 a, 非b, 非c 的其他字符就接受的意思。 |

\[root@oldboy test\]\# echo "$\(date\)"

2016年 03月 27日 星期日 15:56:11 CST

\[root@oldboy test\]\# cp /etc/sysconfig/network-scripts/ifcfg-eth0{,.bak}

\[root@oldboy test\]\# ll /etc/sysconfig/network-scripts/ifcfg-eth0\*

-rw-r--r--. 3 root root 128 3月 20 08:55 /etc/sysconfig/network-scripts/ifcfg-eth0

-rw-r--r-- 1 root root 128 3月 27 16:12 /etc/sysconfig/network-scripts/ifcfg-eth0.bak

\[root@oldboy test\]\# echo {1..5}

1 2 3 4 5

\[root@oldboy test\]\# seq -s " " 5

1 2 3 4 5

\[root@oldboy test\]\# mkdir {1..5}/{a..f} -p

\[root@oldboy test\]\# tree

.

├── 1

│ ├── a

│ ├── b

│ ├── c

│ ├── d

│ ├── e

│ └── f

├── 2

│ ├── a

│ ├── b

│ ├── c

│ ├── d

│ ├── e

│ └── f

├── 3

│ ├── a

│ ├── b

│ ├── c

│ ├── d

│ ├── e

│ └── f

├── 4

│ ├── a

│ ├── b

│ ├── c

│ ├── d

│ ├── e

│ └── f

├── 5

│ ├── a

│ ├── b

│ ├── c

│ ├── d

│ ├── e

│ └── f

├── gongli

├── oldboy.sh

├── oldboy.txt

├── oldgilr.sh

└── test.sh

### 二、重定向符号

#### 1、&gt;或 1&gt;输出重定向，会清楚文件里所有的数据，增加新的内容

#### 2、&gt;&gt; 或 1&gt;&gt; 追加输出重定向，文件的结尾加入内容，不会删除已有的文件数据

#### 3、&lt; 输入重定向

#### 4、&lt;&lt;追加输入重定向

#### 5、2&gt; 错误重定向

#### 6、2&gt;&gt; 错误追加重定向

#### 7、标准输入（stdin）：代码0，使用 &lt; 或 &lt;&lt; 数据流向从右向左

#### 8、标准输出（stdout）: 代码1，使用 &gt; 或 &gt;&gt; 数据流向从左向右

#### 9、标准错误输出（stderr）: 代码2，使用 2&gt; 或 2&gt;&gt; 数据流向从左向右

##### 例子：为oldboy.txt增加内容为“I am studying linux.”

##### 输出重定向

\[root@oldboy data\]\# echo 'I am study linux.' &gt;oldboy.txt

\[root@oldboy data\]\# cat oldboy.txt

I am study linux.

echo 'I am study linux.' &gt;oldboy.txt

##### i、如果没有oldboy.txt，会创建。

##### ii、如果有oldboy.txt，会清空内容，放入单引号的内容。

\[root@oldboy data\]\# echo -e 'I am study linux\nI am study'&gt;&gt;b.txt

\[root@oldboy data\]\# cat b.txt

I am study linux

I am study

\[root@oldboy data\]\# cho "hello oldboy" &gt; all.txt 2&gt;&1

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

\[root@oldboy data\]\# &gt;all.txt

\[root@oldboy data\]\# cat all.txt

\[root@oldboy data\]\# cho "hello oldboy" &&gt; all.txt

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

\[root@oldboy data\]\# &gt; all.txt

\[root@oldboy data\]\# cat all.txt

\[root@oldboy data\]\# cho "hello oldboy" &gt; all.txt 2&gt; all.txt

\[root@oldboy data\]\# cat all.txt

-bash: cho: command not found

##### 输入重定向

echo "1 2 3 4 5" &gt;&gt; /data/oldboy.txt

cat /data/oldboy.txt

1 2 3 4 5

xargs -n2 &lt; /data/oldboy.txt

1 2

3 4

5

\[root@oldboy data\]\# cat b.txt

I am study linux

I am study

\[root@oldboy data\]\# xargs -n1 &lt;b.txt

I

am

study

linux

I

am

study

\[root@oldboy data\]\# xargs -n2 &lt;b.txt

I am

study linux

I am

study

echo oldboy 2&gt;a.txt 1&gt;b.txt

echo oldboy &gt;a.txt 2&gt;&1 错误和正确放在一起

#### 



