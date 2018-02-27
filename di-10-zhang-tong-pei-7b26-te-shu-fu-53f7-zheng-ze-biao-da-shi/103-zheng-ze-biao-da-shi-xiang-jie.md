### 正则表达式  RE regular expression

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

