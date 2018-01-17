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

