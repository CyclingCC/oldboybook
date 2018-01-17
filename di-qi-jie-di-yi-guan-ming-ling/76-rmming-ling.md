#### rm 删除文件或目录 默认只能删文件 -f强制 -r删除目录（递归） {#61-rm---删除文件或目录---默认只能删文件---f强制---r删除目录（递归）}



#### 习惯: 慎用rm 使用mv或者find代替 空间不允许时，先备份，再删除 {#62-习惯-慎用rm--使用mv或者find代替---空间不允许时，先备份，再删除}

#### 进入/root目录下的data目录，删除oldboy.txt文件 {#进入root目录下的data目录，删除oldboytxt文件}

#### 退出到上一级目录，删除data目录 {#退出到上一级目录，删除data目录}

cd /root/data

rm oldboy.txt -f

cd ..

rm /data -r

#### 6.3 修改系统时间 {#63-修改系统时间}

date -s "2016-03-22"

#### 6.4 面试题：删除一个目录下的所有文件，但保留一个指定文件 {#64-面试题：删除一个目录下的所有文件，但保留一个指定文件}

[http://oldboy.blog.51cto.com/2561410/1650380](http://oldboy.blog.51cto.com/2561410/1650380)

解答：

假设这个目录是/xx/，里面有file1,file2,file3..file10 十个文件

\[root@oldboy xx\]\# touch file{1..10}

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

方法一：find

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# find /xx -type f ! -name "file10"\|xargs rm -f

\[root@oldboy xx\]\# ls

file10

\[root@oldboy xx\]\# find /xx -type f ! -name "file10" -exec rm -f {} \;

\[root@oldboy xx\]\# ls

file10

方法二：rsync

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# rsync -az --delete --exclude "file10" /null/ /xx/

\[root@oldboy xx\]\# ls

file10

方法三:开启bash的extglob功能\(此功能的作用就是用rm !\(\*jpg\)这样的方式来删除不包括号内文件的文件\)

\[root@oldboy xx\]\# shopt -s extglob

\[root@oldboy xx\]\# ls

file1 file10 file2 file3 file4 file5 file6 file7 file8 file9

\[root@oldboy xx\]\# rm -f !\(file10\)

\[root@oldboy xx\]\# ls

file10

方法四：

find ./ -type f\|grep -v "\boldboy1\b"\|xargs rm -f

方法五：

rm -f \`ls\|grep -v "\boldboy1\b"\`

#### 从运维角度，任何删除性的操作都应该事先备份后在执行或者确认有备份存在。 {#从运维角度，任何删除性的操作都应该事先备份后在执行或者确认有备份存在。}



