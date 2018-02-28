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



