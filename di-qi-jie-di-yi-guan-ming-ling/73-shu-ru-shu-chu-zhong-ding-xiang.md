#### 输入输出重定向

1. &gt;
    或 1
   &gt;
    输出重定向，会清楚文件里所有的数据，增加新的内容
2. &gt;
   &gt;
    或 1
   &gt;
   &gt;
    追加输出重定向，文件的结尾加入内容，不会删除已有的文件数据
3. &lt;
    输入重定向
4. &lt;
   &lt;
    追加输入重定向
5. 2
   &gt;
    错误重定向
6. 2
   &gt;
   &gt;
    错误追加重定向

1、标准输入（stdin）：代码0，使用 &lt; 或 &lt;&lt; 数据流向从右向左

2、标准输出（stdout）: 代码1，使用 &gt; 或 &gt;&gt; 数据流向从左向右

3、标准错误输出（stderr）: 代码2，使用 2&gt; 或 2&gt;&gt; 数据流向从左向右

### 例子：为oldboy.txt增加内容为“I am studying linux.”

#### 输出重定向

\[root@oldboy data\]\# echo 'I am study linux.' &gt;oldboy.txt

\[root@oldboy data\]\# cat oldboy.txt

I am study linux.

echo 'I am study linux.' &gt;oldboy.txt

1、如果没有oldboy.txt，会创建。

2、如果有oldboy.txt，会清空内容，放入单引号的内容。

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

#### 输入重定向

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

#### cat命令

\[root@oldboy data\]\# cat &gt;a.txt

oldboy

\[root@oldboy data\]\# cat a.txt

oldboy

\[root@oldboy data\]\# cat &gt;&gt;/data/oldboy.txt &lt;&lt;EOF

&gt; I am studying linux.

&gt; EOF

