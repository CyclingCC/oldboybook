### 环境准备

\[root@oldboyedu42-lnb oldboy\]\# cat /oldboy/re.txt

I am oldboy teacher!

I teach linux.



I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448



not 4900000448.

my god ,i am not oldbey,but OLDBOY!

### 一、基础正则

#### 1、^ ^m   表示以....开头的行

\[root@oldboyedu42-lnb oldboy\]\# grep '^m' re.txt 

my blog is http://oldboy.blog.51cto.com 

my qq is 49000448

my god ,i am not oldbey,but OLDBOY!



#### 2、  $  m$  表示以....结尾的行

\[root@oldboyedu42-lnb oldboy\]\# cat -A re.txt

I am oldboy teacher!$

I teach linux.$

$

I like badminton ball ,billiard ball and chinese chess!$

my blog is http://oldboy.blog.51cto.com $          \#注意此处结尾是空格不是m

$

our size is http://blog.oldboyedu.com $            \#注意此处结尾是空格不是m

$

my qq is 49000448$

$

not 4900000448.$

my god ,i am not oldbey,but OLDBOY!$



\#删除结尾的空格

\[root@oldboyedu42-lnb oldboy\]\# vim  re.txt        

  

I am oldboy teacher!

I teach linux.



I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com



our size is http://blog.oldboyedu.com



my qq is 49000448



not 4900000448.

my god ,i am not oldbey,but OLDBOY!



\#检查是否修改成功										 

\[root@oldboyedu42-lnb oldboy\]\# cat -A re.txt           

I am oldboy teacher!$

I teach linux.$

$

I like badminton ball ,billiard ball and chinese chess!$

my blog is http://oldboy.blog.51cto.com$

$

our size is http://blog.oldboyedu.com$

$

my qq is 49000448$

$

not 4900000448.$

my god ,i am not oldbey,but OLDBOY!$

\[root@oldboyedu42-lnb oldboy\]\# 

\[root@oldboyedu42-lnb oldboy\]\# grep 'm$' re.txt 

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com



cat -A  \#显示出文件中所有的符号   $这一行的结尾

\[root@oldboyedu42-lnb oldboy\]\# grep ' '  re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

#### 3、  ^$ 空行 这一行里面什么都没有

\[root@oldboyedu42-lnb oldboy\]\# grep -n '^$'  re.txt 

3:

6:

8:

10:



练习题:排查文件中的空行

\[root@oldboyedu42-lnb oldboy\]\# grep -v '^$' re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!



#### 4、 .  任意一个字符  不会匹配空行

\#grep -o '.' re.txt

\#-o 显示grep的执行过程，grep每一次找出什么

grep -o '.' re.txt

\#-o 显示grep的执行过程，grep每一次找出什么

\#-o 的结果中 每一行表示 grep每次找出什么



\[root@oldboyedu42-lnb oldboy\]\# grep '0' re.txt 

my qq is 49000448

not 4900000448.

\[root@oldboyedu42-lnb oldboy\]\# grep -o '0' re.txt 

0

0

0

0

0

0

0

0

\[root@oldboyedu42-lnb oldboy\]\# grep  '00' re.txt 

my qq is 49000448

not 4900000448.

\[root@oldboyedu42-lnb oldboy\]\# grep -o '00' re.txt 

00

00

00



说明：如果匹配的内容在一行中有多处，grep会从左到右匹配到最后一个，多多益善

提示：点（.）的特殊含义小结：

1、当前目录

2、使得文件生效相当于source

3、隐藏文件的开头

4、任意一个字符



#### 5、 \  撬棍  转义字符  去掉符号特殊含义  脱掉马甲，打回原形

显示出文件中 以.结尾的行？

\[root@oldboyedu42-lnb oldboy\]\# grep '\.$' re.txt 

I teach linux.

not 4900000448.

撬棍系列 转义字符系列

\n  ====== 回车

#### 6、 \*  前一个字符连续出现0次或0次以上

\[root@oldboyedu42-lnb oldboy\]\# grep '0\*' re.txt 

I am oldboy teacher!

I teach linux.



I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com



our size is http://blog.oldboyedu.com



my qq is 49000448



not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboyedu42-lnb oldboy\]\# 

\[root@oldboyedu42-lnb oldboy\]\# grep '0\*' re.txt  -o

000

00000

\#连续出现

\#正则表示连续出现的时候，会尽可能的匹配（吃）更多的符号 贪婪性

\[root@oldboyedu42-lnb oldboy\]\# \#0\* 表示0连续出现0次

\[root@oldboyedu42-lnb oldboy\]\# \#0\* 表示0连续出现1次及1次以上  

\[root@oldboyedu42-lnb oldboy\]\# \#0 

\[root@oldboyedu42-lnb oldboy\]\# \#000

\[root@oldboyedu42-lnb oldboy\]\# \#0000000

\[root@oldboyedu42-lnb oldboy\]\# \#0\* 表示0连续出现0次

\[root@oldboyedu42-lnb oldboy\]\# \#'0\*'  只出现0次的时候  ====== ''

\[root@oldboyedu42-lnb oldboy\]\# \#会把整个文件的内容都显示出来



\[root@oldboyedu42-lnb oldboy\]\# grep ''   re.txt 

I am oldboy teacher!

I teach linux.



I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com



our size is http://blog.oldboyedu.com



my qq is 49000448



not 4900000448.

my god ,i am not oldbey,but OLDBOY!

小结正则之\*：

1\]\] 贪婪性

2\]\] 连续出现

#### 7、 .\*  所有 任何符号

\#在正则中表示连续出现 表示所有 贪婪性

找出文件中以字母m开头的行 并且 以m结尾的行

\[root@oldboyedu42-lnb oldboy\]\# grep '^m'  re.txt 

my blog is http://oldboy.blog.51cto.com

my qq is 49000448

my god ,i am not oldbey,but OLDBOY!

\[root@oldboyedu42-lnb oldboy\]\# grep '^m'  re.txt \|grep 'm$'

my blog is http://oldboy.blog.51cto.com

\[root@oldboyedu42-lnb oldboy\]\# grep '^m.\*m$'  re.txt 

my blog is http://oldboy.blog.51cto.com

\[root@oldboyedu42-lnb oldboy\]\# grep '^.\*m$'  re.txt   

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

\[root@oldboyedu42-lnb oldboy\]\# grep 'm$'  re.txt 

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com



\[root@oldboyedu-42mvp ~\]\# grep '.\*m' re.txt



#### 8、 \[\] \[abc\]  表示一个整体，a或b或c任意一个字符

\[root@oldboyedu42-lnb oldboy\]\# grep '\[abc\]'  re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my god ,i am not oldbey,but OLDBOY!

grep '\[abc\]'  re.txt -o

===&gt;从哪里来，到哪里去用的是-

\[root@oldboyedu42-lnb oldboy\]\# grep '\[a-z\]'  re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboyedu42-lnb oldboy\]\# grep '\[A-Z\]'  re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my god ,i am not oldbey,but OLDBOY!

\[root@oldboyedu42-lnb oldboy\]\# grep '\[a-zA-Z\]'  re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!



\#找出文件中以m或n开头的行 

\[root@oldboyedu42-lnb oldboy\]\# \#第1个里程碑-m或n

\[root@oldboyedu42-lnb oldboy\]\# grep '\[mn\]' re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\[root@oldboyedu42-lnb oldboy\]\# \#第2个里程碑-以m或n开头的行

\[root@oldboyedu42-lnb oldboy\]\# grep '^\[mn\]' re.txt 

my blog is http://oldboy.blog.51cto.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

     

grep '\[a-z\]' re.txt     

grep '\[A-Z\]' re.txt

grep '\[0-9\]' re.txt   



#### 9、 \[^\] 排除  \[^abc\]

\[root@oldboyedu42-lnb ~\]\# grep '\[^abc\]'  /oldboy/re.txt 

I am oldboy teacher!

I teach linux.

I like badminton ball ,billiard ball and chinese chess!

my blog is http://oldboy.blog.51cto.com

our size is http://blog.oldboyedu.com

my qq is 49000448

not 4900000448.

my god ,i am not oldbey,but OLDBOY!

\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|\|000000000

### 二、扩展正则



取出ip地址\(ifconfig ip）

取出文件权限

