##### 管道：前面的输出结果给后面的命令管道后面不支持命令别名 {#管道：前面的输出结果给后面的命令管道后面不支持命令别名}

##### 命令的输出结果经过管道后变成了字符串（数据流），是一个整体 {#命令的输出结果经过管道后变成了字符串（数据流），是一个整体}

\[root@oldboy data\]\# touch {1..10}.txt

\[root@oldboy data\]\# find /data -type f -name "\*.txt"

/data/10.txt

/data/4.txt

/data/8.txt

/data/2.txt

/data/5.txt

/data/6.txt

/data/1.txt

/data/3.txt

/data/9.txt

/data/7.txt

\[root@oldboy data\]\# find /data -type f -name "\*.txt" \|xargs ls -l

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/10.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/1.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/2.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/3.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/4.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/5.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/6.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/7.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/8.txt

-rw-r--r-- 1 root root 0 Mar 13 11:45 /data/9.txt

find /data -type f -name "\*.txt" \|xargs -i mv {} /tmp/

#### 3种方法： {#3种方法：}

cp \`find /data -type f -name "oldboy.txt" -mtime +7\` /tmp/

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

find /data -type f -name "oldboy.txt"\|xargs -i cp {} /tmp/

