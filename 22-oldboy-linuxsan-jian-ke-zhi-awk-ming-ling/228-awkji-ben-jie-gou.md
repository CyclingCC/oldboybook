awk 'BEGIN{}/pattern/{coms}END{coms}'

awk执行过程

1、命令行的赋值（-F 或 -v）

2、执行BEGIN模式里面的内容

3、开始读取文件

4、判断条件（模式）是否成立

成立则执行对应动作里面的内容

读取下一行，循环判断

直到读取到最后一个文件的结尾

5、最后执行END模式里面的内容

6、结束

\[root@nfsserver files\]\# awk -F ":" 'NR==1{print NR,$0}NR==2{print NR,$NF"second line"}' awkfile.txt

1 root:x:0:0:root:/root:/bin/bash

2 /sbin/nologinsecond line

