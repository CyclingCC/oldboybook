awk内置变量（预定义变量）

变量名 属性

$0 当前记录，一整行

$1，$2，$3，...$n 当前记录的第n个字段，字段间由FS分隔

FS 输入字段分隔符 默认是空格

NF 当前记录中的字段个数，就是有多少列

NR 已经读出的记录数，就是行号，从1开始

RS 输入的记录分隔符默认为换行符

OFS 输出字段分隔符 默认是空格

ORS 输出的记录分隔符 默认是换行符

FNR 当前文件的读入记录号

FILENAME 当前正在处理的文件的文件名

\[root@nfsserver files\]\# awk '{print FILENAME,NR,FNR}' awkfile.txt count.txt

awkfile.txt 1 1

awkfile.txt 2 2

awkfile.txt 3 3

awkfile.txt 4 4

awkfile.txt 5 5

awkfile.txt 6 6

awkfile.txt 7 7

awkfile.txt 8 8

awkfile.txt 9 9

awkfile.txt 10 10

count.txt 11 1

count.txt 12 2

count.txt 13 3

count.txt 14 4

count.txt 15 5

count.txt 16 6

count.txt 17 7

count.txt 18 8

count.txt 19 9

count.txt 20 10

