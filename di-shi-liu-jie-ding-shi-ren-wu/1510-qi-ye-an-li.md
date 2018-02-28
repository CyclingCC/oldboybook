#### 1、如果定时任务规则结尾不加&gt;/dev/null 2&gt;&1 或者追加到文件中&gt;&gt;/tmp/oldboy 2&gt;&1，很容易导致硬盘inode空间被占满，从而系统服务不正常

解决方法：

删除大量的小文件/var/spool/postfixdrop/ 下所有的文件

ls \|xargs rm

删除上级目录（看好目录的属性（所有者 组 权限））

临时开启postfix（sendmail）服务（工作中）

#### 2、磁盘不足系列的解决方法

inode满了----定时任务 没有定向到空或文件

block满了

文件硬链接数为0，但是进程占用，所有没有被释放，会越来越多 block

磁盘空间满了：

1. inode满了 df -i

2. block 正常的满了 df -h

   du -sh /\\*

   du -sh /usr/\\*

3. block 非正常的满了 df -h

   du -sh /\* 文件的硬链接数为0，但是还有进程调用。

   lsof \|grep delete



