循环 变量 数组名

for\(key in array\)

关键字

key遍历array数组的下标

11.1 一些实例

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print shou}' awkfile.txt

a

b

c

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print kuang\[shou\]}' awkfile.txt

woman

woman2

woman3

\[root@nfsserver files\]\# awk 'BEGIN{kuang\["a"\]="woman";kuang\["b"\]="woman2";kuang\["c"\]="woman3"}END{for\(shou in kuang\) print shou,kuang\[shou\]}' awkfile.txt

a woman

b woman2

c woman3

11.2 企业面试题

处理以下文件内容，将域名取出并根据域名进行计数排序处理（去重）：（百度和sohu面试题）

\[root@nfsserver files\]\# cat mianshi.txt

[http://www.etiantian.org/index.html](http://www.etiantian.org/index.html)

[http://www.etiantian.org/1.html](http://www.etiantian.org/1.html)

[http://post.etiantian.org/index.html](http://post.etiantian.org/index.html)

[http://mp3.etiantian.org/index.html](http://mp3.etiantian.org/index.html)

[http://www.etiantian.org/3.html](http://www.etiantian.org/3.html)

[http://post.etiantian.org/2.html](http://post.etiantian.org/2.html)

\[root@nfsserver files\]\# awk -F "/+" '{kuang\[$2\]++;print NR,$2,kuang\["www.etiantian.org"\]}' mianshi.txt

1 www.etiantian.org 1

2 www.etiantian.org 2

3 post.etiantian.org 2

4 mp3.etiantian.org 2

5 www.etiantian.org 3

6 post.etiantian.org 3

\[root@nfsserver files\]\# awk -F "/+" '{kuang\[$2\]++}END{for\(shou in kuang\) print shou,kuang\[shou\]}' mianshi.txt

mp3.etiantian.org 1

post.etiantian.org 2

www.etiantian.org 3

\[root@db02 ~\]\# cat sort.txt

[http://www.etiantian.org/index.html](http://www.etiantian.org/index.html)

[http://www.etiantian.org/1.html](http://www.etiantian.org/1.html)

[http://post.etiantian.org/index.html](http://post.etiantian.org/index.html)

[http://mp3.etiantian.org/index.html](http://mp3.etiantian.org/index.html)

[http://www.etiantian.org/3.html](http://www.etiantian.org/3.html)

[http://post.etiantian.org/2.html](http://post.etiantian.org/2.html)

\[root@db02 ~\]\# awk -F "\[/.\]+" '{hotel\[$2\]++}END{for\(police in hotel\)print police,hotel\[police\]}' sort.txt

www 3

mp3 1

post 2

\[root@oldboy files\]\# cat mianshi.txt

[http://www.etiantian.org/index.html](http://www.etiantian.org/index.html)

[http://www.etiantian.org/1.html](http://www.etiantian.org/1.html)

[http://post.etiantian.org/index.html](http://post.etiantian.org/index.html)

[http://mp3.etiantian.org/index.html](http://mp3.etiantian.org/index.html)

[http://www.etiantian.org/3.html](http://www.etiantian.org/3.html)

[http://post.etiantian.org/2.html](http://post.etiantian.org/2.html)

先处理，再输出

\[root@oldboy files\]\# awk -F '\[:/\]+' '{a\[$2\]++}END{for\(i in a\) print a\[i\],i }' mianshi.txt\|sort -r

3 www.etiantian.org

2 post.etiantian.org

1 mp3.etiantian.org

\[root@oldboy36 files\]\# cat url.txt

[http://www.etiantian.org/index.html](http://www.etiantian.org/index.html)

[http://www.etiantian.org/1.html](http://www.etiantian.org/1.html)

[http://post.etiantian.org/index.html](http://post.etiantian.org/index.html)

[http://mp3.etiantian.org/index.html](http://mp3.etiantian.org/index.html)

[http://www.etiantian.org/3.html](http://www.etiantian.org/3.html)

[http://post.etiantian.org/2.html](http://post.etiantian.org/2.html)

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{print $2}' url.txt

www

www

post

mp3

www

post

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["www"\],"www"}' url.txt

3 www

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["post"\],"post"}' url.txt

2 post

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{print h\["mp3"\],"mp3"}' url.txt

1 mp3

\[root@oldboy36 files\]\# awk -F "\[/.\]+" '{h\[$2\]++}END{for\(i in h\)print h\[i\],i}' url.txt

3 www

1 mp3

2 post

\[root@db02 files\]\# awk -F "\[\(\)&lt;&gt;\]" '/^2016/{qi\[$\(NF-1\)\]++}END{for\(key in qi\) print key,qi\[key\]}' 31\_group.txt \|sort -rn -k2

aini8867758258@yahoo.cn 252

2934145242 154

764539136 147

5257409 137

a1046186419@qq.com 121

390320151 99

273558676 96

805022948 85

41117483 82

86988614 79

1226032602 60

10000 57

987766870 56

610010167 54

619876714 41

13216056 40

156322285 37

714900946 36

351319663 36

27061859 36

2051510479 35

1354372178 33

380926619 32

215956299 31

632528468 30

\[root@db02 files\]\# seq 100 \|awk '{sum+=$1}END{print sum}'

5050

11.3 【统计文件中单词个数】\*\*\*\*\*\*\*\*\*

\[root@oldboy files\]\# cat awkfile.txt

root:x:0:0:root:/root:/bin/bash

bin:x:1:1:bin:/bin:/sbin/nologin

daemon:x:2:2:daemon:/sbin:/sbin/nologin

adm:x:3:4:adm:/var/adm:/sbin/nologin

lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

sync:x:5:0:sync:/sbin:/bin/sync

shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown

halt:x:7:0:halt:/sbin:/sbin/halt

mail:x:8:12:mail:/var/spool/mail:/sbin/nologin

uucp:x:10:14:uucp:/var/spool/uucp:/sbin/nologin

\[root@oldboy files\]\# awk -v RS="\[^a-Z\]+" '{a\[$1\]++}END{for\(i in a\) print a\[i\],i}' awkfile.txt \|sort -nr\|column -t

12 sbin

10 x

6 nologin

5 bin

4 var

3 uucp

3 sync

3 spool

3 shutdown

3 root

3 mail

3 halt

3 adm

2 lp

2 daemon

1 lpd

1 bash

11.4 小结

1、awk数组，去重

2、选好分隔符 -F "/+"

3、选好处理的区域，print $1,$3,$2

4、kuang\[$2\]++ =====&gt; a++

5、awk数组的一个处理思想，先处理，最后END模块输出

6、输出awk数组使用for\(shou in kuang\) \#自动摸索

11.5 awk相关英语总结

field 域，区域，字段

record 记录，默认一整行

field separator FS：区域分隔符，表示一个区域的结束，字段，域

number of record NR: 记录号

number of field NF：每一个记录中区域的数量

record separator RS：记录分隔符，标识每个记录的结束

output field separator OFS

output record separator ORS

file number of record FNR awk当前处理的文件的记录号

awk '{h\[$1,$7\]++}END{for\(key in h\) print key,h\[key\]}' filename

深入浅出linux三剑客之awk必杀技一例

[http://oldboy.blog.51cto.com/2561410/950730](http://oldboy.blog.51cto.com/2561410/950730)

