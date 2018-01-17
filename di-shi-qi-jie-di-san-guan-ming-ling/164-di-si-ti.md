#### linux下通过mkdir命令创建一个新目录/oldboy/ett，它的硬链接数是多少，为什么？如果在/oldboy/ett下面再创建一个目录test。再问/oldboy/ett的硬链接数是多少？为什么

\[root@oldboy ~\]\# ls -ld /oldboy/ett/

drwxr-xr-x 2 root root 4096 4月 3 09:35 /oldboy/ett/

硬链接数为2

因为：

1、创建目录本身为一个硬链接

2、ett下隐藏目录.\(点\)为ett目录的又一个硬链接

3、ett下test目录下隐藏文件..\(点点\)也是ett目录的一个硬链接

\[root@oldboy oldboy\]\# ls -ld /oldboy/ett/

drwxr-xr-x 3 root root 4096 Apr 3 11:31 /oldboy/ett/

