#### 三种时间对应关系表

#### column	column	column

#### 访问时间	Access	atime

#### 修改时间	Modify	mtime

#### 状态改动时间	Change	ctime

#### 如何查看文件文件的三种时间戳

#### stat filename

#### 三种时间戳的解释

#### 访问时间：读一次文件的内容，这个时间就会更新。比如more、cat等命令。ls、stat命令不会修改atime

#### 修改时间：修改时间是文件内容最后一次被修改的时间。比如：vim操作后保存文件。ls -l列出的就是这个时间

#### 状态改动时间。是该文件的inode节点最后一次被修改的时间，通过chmod、chown命令修改一次文件属性，这个时间就会更新。

#### 1、mtime 文件内容的最后修改时间

\[root@oldboyedu42-lnb ~\]\# stat oldboy.txt

  File: \`oldboy.txt'

  Size: 69        	Blocks: 8          IO Block: 4096   regular file

Device: 803h/2051d	Inode: 130137      Links: 1

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2017-11-11 08:33:41.661983311 +0800

Modify: 2017-11-11 08:32:43.505972876 +0800

Change: 2017-11-11 08:32:43.505972876 +0800

\[root@oldboyedu42-lnb ~\]\# &gt;oldboy.txt

\[root@oldboyedu42-lnb ~\]\# stat oldboy.txt

  File: \`oldboy.txt'

  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file

Device: 803h/2051d	Inode: 130137      Links: 1

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2017-11-11 08:33:41.661983311 +0800

Modify: 2017-11-11 21:01:21.249962087 +0800

Change: 2017-11-11 21:01:21.249962087 +0800

#### 2、ctime 文件状态的最后更改时间

\[root@oldboyedu42-lnb ~\]\# stat oldboy.txt

  File: \`oldboy.txt'

  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file

Device: 803h/2051d	Inode: 130137      Links: 1

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2017-11-11 08:33:41.661983311 +0800

Modify: 2017-11-11 21:01:21.249962087 +0800

Change: 2017-11-11 21:01:21.249962087 +0800

\[root@oldboyedu42-lnb ~\]\# 

\[root@oldboyedu42-lnb ~\]\# ll oldboy.txt

-rw-r--r-- 1 root root 0 Nov 11 21:01 oldboy.txt

\[root@oldboyedu42-lnb ~\]\# ln oldboy.txt oldboy.txt-hard

\[root@oldboyedu42-lnb ~\]\# ll  oldboy.txt 

-rw-r--r-- 2 root root 0 Nov 11 21:01 oldboy.txt

\[root@oldboyedu42-lnb ~\]\# stat oldboy.txt

  File: \`oldboy.txt'

  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file

Device: 803h/2051d	Inode: 130137      Links: 2

Access: \(0644/-rw-r--r--\)  Uid: \(    0/    root\)   Gid: \(    0/    root\)

Access: 2017-11-11 08:33:41.661983311 +0800

Modify: 2017-11-11 21:01:21.249962087 +0800

Change: 2017-11-11 21:03:09.906964526 +0800

#### 3、atime文件内容最后访问时间



