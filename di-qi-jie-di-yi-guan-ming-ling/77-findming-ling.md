#### find命令格式

find 在哪找\(目录\) 找什么类型\(-type\) 叫什么\(-name\) ... ... ...

find /data -type \[ f d ...\] -name "\*.txt"

#### find 查找文件或目录

\[root@oldboy ~\]\# find / -type f -name "oldgirl.txt"

/data1/oldgirl.txt

find / -type f -name "oldgirl.txt" -exec rm {} \;

find /data -type f -name "oldboy.txt" -mtime +7 -exec rm {} \;

#### 参数

-type f d

-name

-mtime \(+7 7 -7\)

-exec 行动

#### mtime +7 修改时间7天前

find /data -type f -name "oldboy.txt" -mtime +7 -exec cp {} /tmp/ \;

cp \`find /data -type f -name "oldboy.txt"\` /tmp/

#### 企业面试题：查找/oldboy下所有7天前的以log结尾的文件移动到/tmp下

find /oldboy/ -type f -name "\*.log" -mtime +7 -exec mv {} /tmp/ \;

[http://oldboy.blog.51cto.com/2561410/1750481](http://oldboy.blog.51cto.com/2561410/1750481)

