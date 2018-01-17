#### ls -lhi

7 8 9 三列是时间（默认是修改时间）

modify mtime 文件内容修改时间

change ctime 文件属性改变时间

access atime 文件内容访问时间

#### 查看文件属性详细信息

\[root@oldboy36 ~\]\# stat /etc/hosts

File: "/etc/hosts"

Size: 158 Blocks: 8 IO Block: 4096 普通文件

Device: 803h/2051d Inode: 654109 Links: 1

Access: \(0644/-rw-r--r--\) Uid: \( 0/ root\) Gid: \( 0/ root\)

Access: 2017-05-15 18:05:01.727193092 +0800

Modify: 2010-01-12 21:28:22.000000000 +0800

Change: 2017-05-01 12:07:24.733999989 +0800

