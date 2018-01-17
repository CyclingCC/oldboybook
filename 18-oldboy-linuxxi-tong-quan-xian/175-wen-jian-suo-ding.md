#### 文件锁定

\[root@oldboy ~\]\# chattr +i /etc/passwd

-a 文件内容只能增加

\[root@oldboy ~\]\# chattr +a /etc/passwd

#### 文件解锁

\[root@oldboy ~\]\# chattr -i /etc/passwd

查看文件锁定情况：

\[root@oldboy ~\]\# lsattr /etc/passwd

----i--------e- /etc/passwd





