#### 1、简单粗暴/etc/rc.local

所有你想启动的脚本或服务，把他们启动的命令放入/etc/rc.local这个文件中即可。

启动的时候注意下启动顺序，比如说nfs和rpcbind\(Portmap\)服务。

#### 2、专业的管理工具chkconfig

Chkconfig管理一个服务或脚本让他开机自启动有下面几个条件:

1）这个服务或脚本必须存放在/etc/init.d目录下面

2）必须要有执行权限\(x权限\)

3）这个脚本或服务的前几行必须要有

\# chkconfig: 2345 99 99必须要有这一行否则chkconfig不认识

\#\[空格\]chkconfig:\[空格\]默认在哪个运行级别启动这个服务或软件\[空格\]第几个开机启动的\[空格\]关机的顺序

4）chkconfig --add服务名字/脚本名字把服务或脚本加入到chkconfig管理之中。

注：这里主要写清楚通过/etc/rc.local和chkconfig管理即可。

![](/assets/19-4.jpg)

