### 扩展的正则表达式 {#16--扩展的正则表达式}

* 匹配前面一个字符一次或多次

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

###  {#17--正则表达式特殊符号}



