# 第1章 正则表达式

用于匹配字符串

### 1.1  grep命令

grep  \[OPTIONS\]  PATTERN  \[FILE...\]



| **参数** | **参数说明** | **其他说明** |
| :--- | :--- | :--- |
| **-o** | **仅显示匹配的内容** |  |
| **-i** | **忽略大小写** |  |
| **-n** | **显示行号** |  |
| **-v** | **反向选择** |  |
| **-E** | **扩展的grep** |  |
| **--color=auto** | **以颜色高亮显示匹配关键字** |  |
| **-A** | **显示匹配字符串及其后n行** |  |
| **-B** | **显示匹配字符串及其前n行** |  |
| **-C** | **显示匹配字符串及其前后各n行** |  |
| **-w** | **匹配单词** |  |
| **-c** | **显示匹配次数** |  |
| **-m** | **匹配地几个** | **-m 5** |
| **-a** | **在二进制文件中，以文本文件方式搜索** |  |

cat &gt;&gt; /etc/bashrc &lt;&lt; EOF

alias egrep='egrep --color=auto'

alias grep='grep --color=auto'

EOF

linux正则表达式与通配符揉碎剁烂实战讲解视频课程

[http://edu.51cto.com/course/course\_id-7001.html](http://edu.51cto.com/course/course_id-7001.html)

### 1.2 基础正则表达式（Basic RegEx）与扩展正则表达式（Extended RegEx）



| **元字符** | **描述** | **例子** | **BRE** | **ERE** |
| :--- | :--- | :--- | :--- | :--- |
| **^** | 匹配行首 | ^abc匹配已abc开头的行 | ^ | ^ |
| **$** | 匹配行尾 | test$匹配已test结尾的行 | $ | $ |
| **.** | 匹配任意一个字符 | ^al..num$匹配已al开头，num结尾，中间2个任意字符的行 | . | . |
| **\[\]** | 匹配中括号之中任意一个字符 | a\[upe\]b匹配aub,apb,aebde\[0-9\]l匹配de0l,de1l,de2l,...,de9l | \[ \] | \[ \] |
| **\[^\]** | 匹配中括号内字符之外任意一个字符 | add\[^12\]不匹配add1,add2,可以匹配add3,adda,add6等等，不在括号中的字符即可 | \[^\] | \[^\] |
| **\*** | 匹配前一个项0次或多次 | ab\*c匹配ac,abc,abbbc等等,.\*表示任意个任意字符 | \* | \* |
| **?** | 匹配前一个项0次或1次 | ab?c匹配ac，abc | \? | ? |
| **+** | 匹配前一个项1次或多次 | ab+c匹配abc,abbbbc等 | \+ | + |
| **\(\)** | 分组，子表达式组合，创建一个匹配字串 | test\(oldboy\)?匹配test,testoldboy | \\(\\) | \(\) |
| **{m}** | 匹配前一个项m次 | \(test\){2}匹配testtest\[a-z\]{5}匹配任意5位小写字母 | \{m\} | {m} |
| **{m,n}** | 匹配前一个项至少m次，至多n次 | \(lidao\){1,2}匹配lidao,lidaolidao\[0-9\]{5,10}匹配任意5位至10位数字 | \{m,n\} | {m,n} |
| **{,n}** | 匹配前一个项至多n次 | abc\(123\){,2}匹配abc,abc123,abc123123 | \{,n\} | {,n} |
| **{m,}** | 匹配前一个项至少m次 | \[0-9\]{5,}匹配5位或以上的任意数字 | \{m,\} | {m,} |
| **\|** | 或的意思，匹配2边任意一项 | lol\(mysql\|lnmp\)匹配lolmysql,lollnmp | \\| | \| |
| **\** | 转义符，忽略特殊字符的特殊意义，显示其本身 | netstat\.匹配netstat.,不匹配netstatt | \ | \ |

 

基本正则    grep   sed

扩展的正则   egrep    sed -r   awk

适合linux三剑客

以行为单位处理

cat &gt;&gt;/etc/profile&lt;&lt;EOF

alias egrep='egrep --color=auto'

alias grep='grep --color=auto'

EOF

source  /etc/profile

export LC\_ALL=C

测试文件

cat &gt;&gt;~/test/oldboy.log&lt;&lt;EOF

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

our site is  [http://www.etiantian.org](http://www.etiantian.org)

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

### 1.3 基础正则\(BRE\)第一波字符说明

1、  ^word   匹配开头word

2、  word$   匹配word结尾

3、  ^$      匹配开头结尾   即空行

\[root@oldboy test\]\# grep "^m" oldboy.log

my blog is [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

my qq num is 49000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy test\]\# grep "m$" oldboy.log

my blog is [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

\[root@oldboy test\]\# grep -n "^$" oldboy.log

3:

8:

\[root@oldboy36 test\]\# grep "^m" oldboy.log

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

my qq num is 49000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^$" oldboy.log

3:

8:

\[root@oldboy36 test\]\# grep "oldboy" oldboy.log

I am oldboy teacher!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

\[root@oldboy36 test\]\# grep "oldb.y" oldboy.log

I am oldboy teacher!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "oldb.y" oldboy.log -o

oldboy

oldboy

oldbey

\[root@oldboy36 test\]\# grep ".$" oldboy.log

I teach linux.

my qq num is 49000448.

not 4900000448.

### 1.4 基础正则（BRE）第二波字符说明

.   代表且只能代表任意一个字符

转译符号，特殊字符还原本意

\n  表示换行

\n 在  echo  sed  awk 中使用

\*   匹配前面的一个字符0次或多次（任意多次）

.\*   匹配任意一个字符任意多次（任意字符串）

^.\*  匹配开头任意字符串

\[root@oldboy36 test\]\# grep "^.\*o" oldboy.log

I am oldboy teacher!

I like badminton ball ,billiard ball and chinese chess!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

our site is  [http://www.etiantian.org](http://www.etiantian.org)

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

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

\[root@oldboy36 test\]\# grep -n "." oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n ".\*" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

3:

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

8:

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

### 1.5 基础正则（BRE）第三波字符说明

\[abc\]   匹配a、b、c任意一个字符

\[^abc\]  匹配非a、非b、非c 任意一个字符

a{n,m}  匹配a这个字符 n到m次

a{n,}    匹配a这个字符至少n次

a{n}    匹配a这个字符n次

a{,m}   匹配a这个字符最多m次

注意： 上面的  是转义 ，但是在 egrep  \(grep -E\) 或 sed -r  或  awk   {}  不需要转义

\[root@oldboy36 test\]\# grep -n "\[abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "\[a-Z0-9\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^\[abc\]" oldboy.log

\[root@oldboy36 test\]\# grep -n "\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep -n "^\[^abc\]" oldboy.log

1:I am oldboy teacher!

2:I teach linux.

4:I like badminton ball ,billiard ball and chinese chess!

5:my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

6:our site is  [http://www.etiantian.org](http://www.etiantian.org)

7:my qq num is 49000448.

9:not 4900000448.

10:my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[^a-z\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

our site is  [http://www.etiantian.org](http://www.etiantian.org)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep "\[^0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

our site is  [http://www.etiantian.org](http://www.etiantian.org)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep  "\[^0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

our site is  [http://www.etiantian.org](http://www.etiantian.org)

my qq num is 49000448.

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep  -v "\[0-9\]" oldboy.log

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

our site is  [http://www.etiantian.org](http://www.etiantian.org)

my god ,i am not oldbey,but OLDBOY!

\[root@oldboy36 test\]\# grep  "\[0-9\]" oldboy.log

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

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

### 1.6  扩展的正则表达式

+      匹配前面一个字符一次或多次

a+   匹配a这个字符一次或多次

?     匹配前面一个字符0次或1次

a?   匹配a这个字符0次或1次

\|   表示或者  用于同时过滤多个

\( \)  分组  后向引用

egrep "0+" oldboy.txt

egrep -o "0+" oldboy.txt

egrep -o "\[a-z\]+" oldboy.txt

egrep  "\[a-z\]+" oldboy.txt

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

Inode size:              128

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "block size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size:               1024

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "inode count"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              51200

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|grep -i "block count"

dumpe2fs 1.41.12 \(17-May-2010\)

Block count:              204800

Reserved block count:     10240

\[root@oldboy36 ~\]\# echo "\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*" \|egrep "\[\#@\*\]+"

\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*

\[root@oldboy36 ~\]\# echo "\#\#\*\*\#\#@@\#\#@\#\#\*\#1@@@@@@@2\*\*@@@\*\*\#\#\*\*" \|egrep "\[\#@\*\]+" -o

\#\#\*\*\#\#@@\#\#@\#\#\*\#

@@@@@@@

\*\*@@@\*\*\#\#\*\*

\[root@oldboy36 test\]\# egrep "oldb\(o\|e\)y" oldboy.log

I am oldboy teacher!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

my god ,i am not oldbey,but OLDBOY!

oldboy1

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size:               1024

Inode size:              128

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) count"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              51200

Block count:              204800

Reserved block count:     10240

\[root@oldboy36 test\]\# dumpe2fs /dev/sda1 \|egrep -i "\(inode\|block\) \(size\|count\)"

dumpe2fs 1.41.12 \(17-May-2010\)

Inode count:              51200

Block count:              204800

Reserved block count:     10240

Block size:               1024

Inode size:              128

### 1.7  正则表达式特殊符号



| 正则表达式 | 描述 | 示例 |
| :--- | :--- | :--- |
| \b | 单词边界 | \bcool\b只匹配cool |
| \B | 非单词边界 | cool\B匹配coolxxxx ,不匹配cool |
| \d | 一个数字字符 |  |
| \D | 一个非数字字符 |  |
| \w | 一个单词（连续字符） |  |
| \W | 一个非单词 |  |
| \n | 换行符 |  |
| \s | 一个空白字符 |  |
| \S | 一个非空白字符 |  |
| \r | 回车 |  |
| \t | 横向制表符（tab） |  |
| \v | 垂直制表符 |  |
| \f | 换页符 |  |

 

\[root@oldboy36 test\]\# echo oldboy1 &gt;&gt; oldboy.log

\[root@oldboy36 test\]\# grep "\boldboy\b" oldboy.log

I am oldboy teacher!

my blog is  [http://oldboy.blog.51cto.com](http://oldboy.blog.51cto.com)

\[root@oldboy ~\]\# cat -nA test.txt

```
 1  asdfsfasfasf$

 2  $                           &lt;=========这个是空行

 3  asdfsf$

 4  sdfasfsa$

 5     $                        &lt;=========这行全是空格

 6  sdfasdfas$

 7  ^I$                         &lt;=========这行是tab键

 8  asdfsad$
```

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

### 1.8  空行的处理

egrep -v "^$"  /oldboy/test.txt

sed '/^$/d'  /oldboy/test.txt

awk '/^$/' /oldboy/test.txt

awk '!/^$/' /oldboy/test.txt

### 1.9  企业案例

\[root@oldboy oldboy\]\# find /root/oldboy -type f\|xargs sed -i '/&lt;script language=javascript src=http:\/\/%4%66E%78%6F%72%67%2E%70%6F\/x.js?google\_ad=93x28\_ad&gt;&lt;\/script&gt;/d'

\[root@oldboy oldboy\]\# find /root/oldboy -type f\|xargs sed -i 's\#&lt;script language=javascript src=[http://%4%66E%78%6F%72%67%2E%70%6F/x.js?google\_ad=93x28\_ad&gt;&lt;/script&gt;\#\#g](http://%4%66E%78%6F%72%67%2E%70%6F/x.js?google_ad=93x28_ad></script>##g)'

### 1.10  取出/etc/passwd中的第一列

egrep -o "^\[a-zA-Z0-9\]+" /etc/passwd

egrep -o "^\[^:\]+" /etc/passwd

sed -r  's\#\(^\[a-zA-Z0-9\#\]+\).\*$\#\1\#g' /etc/passwd

sed -r  's\#\(^\[^:\]+\).\*$\#\1\#g' /etc/passwd

### 1.11  交换/etc/passwd中第一列与最后一列位置

sed -r 's\#\(^\[a-zA-Z0-9\#\]+\)\(:.\*:\)\(.\*$\)\#\3\2\1\#g' /etc/passwd

sed -r 's\#\(^\[^:\]+\)\(:.\*:\)\(.\*$\)\#\3\2\1\#g' /etc/passwd

\[root@oldboy ~\]\# sed -rn 's\#\(^\[^:\]+\)\(:.\*:\)\(.\*\)\#\3\2\1\#gp' /etc/passwd\|head

/bin/bash:x:0:0:root:/root:root

/sbin/nologin:x:1:1:bin:/bin:bin

/sbin/nologin:x:2:2:daemon:/sbin:daemon

/sbin/nologin:x:3:4:adm:/var/adm:adm

/sbin/nologin:x:4:7:lp:/var/spool/lpd:lp

/bin/sync:x:5:0:sync:/sbin:sync

/sbin/shutdown:x:6:0:shutdown:/sbin:shutdown

/sbin/halt:x:7:0:halt:/sbin:halt

/sbin/nologin:x:8:12:mail:/var/spool/mail:mail

/sbin/nologin:x:10:14:uucp:/var/spool/uucp:uucp

