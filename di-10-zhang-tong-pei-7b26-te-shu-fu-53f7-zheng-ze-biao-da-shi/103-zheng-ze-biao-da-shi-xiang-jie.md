### 一、正则表达式  RE regular expression

#### 1、什么是正则 为何用它？

你可以通过什么方法选出这里面的身份证号码。

440304199604012792

130528197108126121

3605sss98304033896

342923198310042132

1404ddddddddd5694X

61242619860416291X

5002xxxxxx04279521

330900199806382320

654126197703092303

131127197105115662

数字与X\(在最后一位\)

通过符号匹配查找出各种文字。

正则表达式通过特殊符号 ^ $ \[\] . \*  表示各种各样的文字。

方便我们处理文本（日志）。

#### 2、正则使用范围

谁可以使用正则？

三剑客正则\(grep sed awk \)

python java

#### 3、正则表达式与通配符区别

正则-----在文件中进行过滤（查找文件内容）    三剑客支持

通配符---找出文件（文件名）                大部分命令都可以使用

#### 4、使用正则注意事项

1\) 正则默认是按照行为单位处理。

2\) 一定要注意不要使用中文符号。

. ''""^ \`\` \( \) {} \[\]   &lt;&gt;

。‘’“”……••（ ）{}【】《》

3\) 给grep/egrep加上别名

cat &gt;&gt;/etc/profile&lt;&lt;EOF

alias grep='grep --color=auto'

alias egrep='egrep --color=auto'

EOF

source /etc/profile

#### 5、正则分类

基础正则: ^  $ . \*  \[\]

扩展正则: +  \| \(\)  {}  ?

![](/assets/15-2.png)![](/assets/15-3.png)基本正则 grep sed

扩展的正则 egrep sed -r awk

适合linux三剑客

以行为单位处理

cat &gt;&gt;/etc/profile&lt;&lt;EOF

alias egrep='egrep --color=auto'

alias grep='grep --color=auto'

EOF

source /etc/profile

export LC\_ALL=C

测试文件

cat &gt;&gt;~/test/oldboy.log&lt;&lt;EOF

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

our site is[http://www.etiantian.org](http://www.etiantian.org/)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

gd

good

god

goood

gooood

oldboy1

EOF

### 二、基础正则

#### 基础正则\(BRE\)第一波字符说明

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

### 三、扩展正则

. 匹配前面一个字符一次或多次

a+ 匹配a这个字符一次或多次

? 匹配前面一个字符0次或1次

a? 匹配a这个字符0次或1次

\| 表示或者 用于同时过滤多个

\( \) 分组 后向引用

egrep "0+" oldboy.txt

egrep -o "0+" oldboy.txt

egrep -o "\[a-z\]+" oldboy.txt

egrep "\[a-z\]+" oldboy.txt

egrep -o "\[a-z\]+" oldboy.txt

egrep -o "\[a-zA-Z\]+" oldboy.txt

egrep -o "\[a-Z\]+" oldboy.txt

\[root@oldboy36 test\]\# egrep "go?d" oldboy.log

my god ,i am not oldbey,but OLDBOY!

gd

god

\[root@oldboy36 test\]\# egrep "go+d" oldboy.log

my god ,i am not oldbey,but OLDBOY!

good

god

goood

gooood

\[root@oldboy36 test\]\# egrep "go\*d" oldboy.log

my god ,i am not oldbey,but OLDBOY!

gd

good

god

goood

gooood

\[root@oldboy36 test\]\# egrep "go{0,3}d" oldboy.log

my god ,i am not oldbey,but OLDBOY!

gd

good

god

goood

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "inode size"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode size: 128

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "block size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size: 1024

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "inode count"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count: 51200

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "block count"

dumpe2fs 1.41.12 \(17-May-2010\)

Block count: 204800

Reserved block count: 10240

\[root@oldboy36 ~\]\# echo "\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*" \|egrep "\[\#@\*\]+"

\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*

\[root@oldboy36 ~\]\# echo "\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*" \|egrep "\[\#@\*\]+" -o

\#\#\*\*\#\#@@\#\#@\#\#\*\#

@@@@@@@

\*\*@@@\*\*\#\#\*\*

\[root@oldboy36 test\]\# egrep "oldb\(o\|e\)y" oldboy.log

I am oldboy teacher!

my blog is[http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com/)

my god ,i am not oldbey,but OLDBOY!

oldboy1

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size: 1024

Inode size: 128

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) count"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count: 51200

Block count: 204800

Reserved block count: 10240

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) \(size\|count\)"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count: 51200

Block count: 204800

Reserved block count: 10240

Block size: 1024

Inode size: 128

