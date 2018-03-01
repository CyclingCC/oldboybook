#### 一、10句箴言

#### 1、需要修改系统环境变量问题

export PATH

1）命令的绝对路径

2）在脚本中，修改使用的PATH

export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

#### 2、定时任务要用绝对路径

#### 3、 定时任务的脚本权限问题

/bin/sh shell的脚本

#### 4、 时间变量问题用反斜线

cd /&& tar zcf /data/html\_$\(date +\%F-\%M-\%H-%S\).tar.gz var/www/

#### 5、定时任务里面的命令或脚本要定向到空或指定个文件

/dev/null 2&gt;&1 或者 &gt;&gt; /server/log/ip.log 2&gt;&1

#### 6、定时任务规则之前加注释

#### 7、 使用脚本程序替代命令行定时任务

#### 8、 避免不必要的程序及命令输出

#### 9、 打包压缩使用相对路径（切到目录目录的上一级打包目标）

#### 10、 定时任务脚本中的程序命令及路径尽量用全路径

### 二、故障案例

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

1）inode满了 df -i

2）block 正常的满了 df -h

du -sh /\\*

du -sh /usr/\\*

3）block 非正常的满了 df -h

du -sh /\* 文件的硬链接数为0，但是还有进程调用。

lsof \|grep delete



