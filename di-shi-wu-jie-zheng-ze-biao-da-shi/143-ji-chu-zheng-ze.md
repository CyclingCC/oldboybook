####  基础正则\(BRE\)第一波字符说明

1、 ^word 匹配开头word

2、 word$ 匹配word结尾

3、 ^$ 匹配开头结尾 即空行

\[root@oldboy test\]\# grep "^m" oldboy.log

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

my qq num is 49000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy test\]\# grep "m$" oldboy.log

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

\[root@oldboy test\]\# grep -n "^$" oldboy.log

3:

8:

\[root@oldboy36 test\]\# grep "^m" oldboy.log

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

my qq num is 49000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^$" oldboy.log

3:

8:

\[root@oldboy36 test\]\# grep "oldboy" oldboy.log

I am oldboy teacher!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

\[root@oldboy36 test\]\# grep "oldb.y" oldboy.log

I am oldboy teacher!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "oldb.y" oldboy.log -o

oldboy

oldboy

oldbey

\[root@oldboy36 test\]\# grep ".$" oldboy.log

I teach linux.

my qq num is 49000448.

not 4900000448.

#### 基础正则（BRE）第二波字符说明

. 代表且只能代表任意一个字符

转译符号，特殊字符还原本意

\n 表示换行

\n 在 echo sed awk 中使用

\* 匹配前面的一个字符0次或多次（任意多次）

.\* 匹配任意一个字符任意多次（任意字符串）

^.\* 匹配开头任意字符串

\[root@oldboy36 test\]\# grep "^.\*o" oldboy.log

I am oldboy teacher!

I like badminton ball ,billiard ball and chinese chess!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

our site is[http://www.etiantian.org](http://www.etiantian.org/)

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

说明：如果匹配的内容在一行中有多处，grep会从左到右匹配到最后一个，多多益善

提示：点（.）的特殊含义小结：

1、当前目录

2、使得文件生效相当于source

3、隐藏文件的开头

4、任意一个字符

\[root@oldboy36 test\]\# grep -n "." oldboy.log

2:I teach linux.

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

\[root@oldboy36 test\]\# grep -n "." oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n ".\*" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

3:

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

8:

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

#### 基础正则（BRE）第三波字符说明

\[abc\] 匹配a、b、c任意一个字符

\[^abc\] 匹配非a、非b、非c 任意一个字符

a{n,m} 匹配a这个字符 n到m次

a{n,} 匹配a这个字符至少n次

a{n} 匹配a这个字符n次

a{,m} 匹配a这个字符最多m次

注意： 上面的 是转义 ，但是在 egrep \(grep -E\) 或 sed -r 或 awk {} 不需要转义

\[root@oldboy36 test\]\# grep -n "\[abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "\[a-Z0-9\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^\[abc\]" oldboy.log

\[root@oldboy36 test\]\# grep -n "\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

6:our site is[http://www.etiantian.org](http://www.etiantian.org/)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[^a-z\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

our site is[http://www.etiantian.org](http://www.etiantian.org/)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[^0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

our site is[http://www.etiantian.org](http://www.etiantian.org/)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[^0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

our site is[http://www.etiantian.org](http://www.etiantian.org/)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -v "\[0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

our site is[http://www.etiantian.org](http://www.etiantian.org/)

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[0-9\]" oldboy.log

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

my qq num is 49000448.

not 4900000448.

\[root@oldboy36 test\]\# grep "0{2,3}" oldboy.log

my qq num is 49000448.

not 4900000448.

\[root@oldboy36 test\]\# grep -o "0{2,3}" oldboy.log

000

000

00

\[root@oldboy36 test\]\# grep "0{1,5}" oldboy.log

my qq num is 49000448.

not 4900000448.

\[root@oldboy36 test\]\# grep -o "0{1,5}" oldboy.log

000

00000

\[root@oldboy36 test\]\# egrep "0{1,5}" oldboy.log

my qq num is 49000448.

not 4900000448.

\[root@oldboy36 test\]\# egrep -o "0{1,5}" oldboy.log

000

00000

