### 正则表达式特殊符号 {#17--正则表达式特殊符号}

![](https://www.luffycity.com/linux-book/assets/15-4.png)

\[root@oldboy36 test\]\# echo oldboy1 &gt;&gt; oldboy.log

\[root@oldboy36 test\]\# grep "\boldboy\b" oldboy.log

I am oldboy teacher!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

\[root@oldboy ~\]\# cat -nA test.txt

1  asdfsfasfasf$

2  $                           &lt;=========这个是空行

3  asdfsf$

4  sdfasfsa$

5     $                        &lt;=========这行全是空格

 6  sdfasdfas$

 7  ^I$                        &lt;=========这行是tab键

 8  asdfsad$



\[root@oldboy ~\]\# egrep "^\s\*$" test.txt -n

2:

5:

7:

\[root@oldboy ~\]\# egrep "^\s\*$" test.txt -nv

1:asdfsfasfasf

3:asdfsf

4:sdfasfsa

6:sdfasdfas

8:asdfsad

\[root@oldboy ~\]\# sed -rn '/^\[ \t\]\*$/{=;p}' test.txt

2

5

7

\[root@oldboy ~\]\# sed -r '/^\[ \t\]\*$/d' test.txt

asdfsfasfasf

asdfsf

sdfasfsa

sdfasdfas

asdfsad

