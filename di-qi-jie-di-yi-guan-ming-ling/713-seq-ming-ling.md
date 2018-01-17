Linux 中一个预设的外部命令，一般用作一堆数字的简化写法

\[root@oldboy data\]\# seq 1 2 9 \|xargs

1 3 5 7 9

\[root@oldboy data\]\# seq -s " " 5

1 2 3 4 5

\[root@oldboy data\]\# seq -s "-" 5

1-2-3-4-5

