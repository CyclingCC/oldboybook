#### mv命令格式

mv \[OPTION\]... SOURCE... DIRECTORY

mv \[选项\]... 文件（或目录）... 目录

mv \[OPTION\]... -t DIRECTORY SOURCE...

mv \[选项\]... -t 目录 文件（或目录）

#### mv 移动文件或目录（改名）

把/data目录移动到/root下

\[root@oldboy tmp\]\# mv /data /root/

\[root@oldboy tmp\]\# mkdir stu{11..20}

\[root@oldboy tmp\]\# ls

oldboy.txt stu12 stu14 stu16 stu18 stu20

stu11 stu13 stu15 stu17 stu19

\[root@oldboy tmp\]\# mkdir \`seq 10\`

\[root@oldboy tmp\]\# ls

1 2 4 6 8 oldboy.txt stu12 stu14 stu16 stu18 stu20

10 3 5 7 9 stu11 stu13 stu15 stu17 stu19

#### 操作习惯

目录下的内容，不包括目录data本身

mv /data/\* /tmp/

目录及下面的内容，包含目录 data本身

mv /data /tmp/

实际上 cp mv 源/data和/data/一致，目标/tmp如果不存在就把/data改为/tmp

rsync特殊

