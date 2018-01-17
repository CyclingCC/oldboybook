#### cp 拷贝文件或目录 默认只能拷贝文件

#### cp命令格式

cp \[OPTION\]... SOURCE... DIRECTORY

cp \[选项\] 文件（或目录）... 目录

cp \[OPTION\]... -t DIRECTORY SOURCE...

cp \[选项\] -t 目录 文件（或目录）...

#### 参数选项

-r \(递归\) 拷贝目录

-p 保持属性

-a 完全拷贝 相当于 -pdr

### 把oldboy.txt文件拷贝到/tmp下

cp /data/oldboy.txt /tmp/

cp -r /data /tmp/

#### 已知/tmp下已经存在test.txt文件，如何执行命令才能把/mnt/test.txt拷贝到/tmp下覆盖掉/tmp/test.txt，而让系统不提示是否覆盖，cp不提示：

\[root@oldboy oldboy\]\# cp a.txt /tmp/

cp: overwrite \`/tmp/a.txt'? y

\[root@oldboy oldboy\]\# \cp a.txt /tmp/

\[root@oldboy oldboy\]\# /bin/cp a.txt /tmp/

