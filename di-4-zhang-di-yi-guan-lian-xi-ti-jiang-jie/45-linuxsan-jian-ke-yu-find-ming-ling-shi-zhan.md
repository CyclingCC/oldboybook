#### 例子：/oldboy目录下文件中内容oldboy替换为oldgirl

##### 1、创建环境

mkdir -p /oldboy/test

cd /oldboy

echo "oldboy"&gt;test/del.sh

echo "oldboy"&gt;test.sh

echo "oldboy"&gt;t.sh

touch oldboy.txt

touch alex.txt

##### 2、找出文件

\[root@oldboyedu36 oldboy\]\# \#找到你要处理的东西

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f

/oldboy/alex.txt

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/oldboy.txt

/oldboy/t.sh

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

##### 3、把一个文件中的oldboy替换为oldgirl

sed 's\#找谁\#替换成啥\#g'

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

oldgirl

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldboy

\[root@oldboyedu36 oldboy\]\# sed -i 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldgirl

##### 4、用find命令找到文件，然后用sed修改文件内容

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

\[root@oldboyedu36 oldboy\]\# \#\#先看看结果对不对

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh^C

\[root@oldboyedu36 oldboy\]\# sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh^C

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"\|xargs sed 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

oldgirl

oldgirl

oldgirl

oldgirl

\[root@oldboyedu36 oldboy\]\# \#\#结果对了 -i

\[root@oldboyedu36 oldboy\]\# find /oldboy/ -type f -name "\*.sh"\|xargs sed -i 's\#oldboy\#oldgirl\#g' /oldboy/test.sh

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test.sh

oldgirl

\[root@oldboyedu36 oldboy\]\# cat /oldboy/test/del.sh

oldgirl

##### 5、其它方法

方法二

\[root@oldboyedu36 ~\]\# \#\#\#

\[root@oldboyedu36 ~\]\# which mkdir

/bin/mkdir

\[root@oldboyedu36 ~\]\# ls -l /bin/mkdir

-rwxr-xr-x. 1 root root 50056 Mar 23 02:52 /bin/mkdir

\[root@oldboyedu36 ~\]\#

\[root@oldboyedu36 ~\]\# \#\#\#把上面两条命令合起来

\[root@oldboyedu36 ~\]\# \#\#\#ls -l 此处放置的是which mkdir命令的结果

\[root@oldboyedu36 ~\]\# ls -l which mkdir

ls: cannot access which: No such file or directory

ls: cannot access mkdir: No such file or directory

\[root@oldboyedu36 ~\]\# ls -l $\(which mkdir\)

-rwxr-xr-x. 1 root root 50056 Mar 23 02:52 /bin/mkdir

\[root@oldboyedu36 ~\]\# \#\#$\(\) 表示 先执行里面的"命令",然后把命令结果留下来

\[root@oldboyedu36 ~\]\# \#\#$\(\) ===== \`\`

$\(\) &lt;==&gt; \`\` 在一个命令中包含另一个命令

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g' 文件名字 文件 文件 文件

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g' 这些文件怎么得到的？

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g' find命令的结果

\[root@oldboyedu36 ~\]\# \#sed 's\#oldboy\#oldgirl\#g' $\(find /oldboy/ -type f -name "\*.sh"\)

\[root@oldboyedu36 ~\]\# sed 's\#oldboy\#oldgirl\#g' $\(find /oldboy/ -type f -name "\*.sh"\)

oldgirl

oldgirl

oldgirl

方法三

\[root@oldboyedu36 ~\]\# \#\#\#

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh"

/oldboy/test.sh

/oldboy/test/del.sh

/oldboy/t.sh

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh" -exec ls -l {} \;

-rw-r--r--. 1 root root 7 May 3 06:27 /oldboy/test.sh

-rw-r--r--. 1 root root 7 May 3 06:27 /oldboy/test/del.sh

-rw-r--r--. 1 root root 7 May 3 06:27 /oldboy/t.sh

\[root@oldboyedu36 ~\]\# find /oldboy/ -type f -name "\*.sh" -exec sed 's\#oldboy\#oldgirl\#g' {} \;

oldgirl

oldgirl

oldgirl

##### 6、修改网卡ip

find /etc/ -type f -name "\*eth0" \|xargs sed 's\#IPADDR=.\*\#IPADDR=10.0.0.200\#'

