#### 1、使用命令调换 passwd 文件里 root 位置和/bin/bash 位置？ 即将所有的第一列和最后一列位置调换？

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

修改后： 

```
/bin/bash:x:0:0:root:/root:root
/sbin/nologin:x:1:1:bin:/bin:bin
/sbin/nologin:x:2:2:daemon:/sbin:daemon
/sbin/nologin:x:3:4:adm:/var/adm:adm
/sbin/nologin:x:4:7:lp:/var/spool/lpd:lp
```

#### 2、test.txt内容为:

```
trainning

fanbingbing

lidao
```

请给出输出test.txt文件内容时，不显示文件中的空行。（至少2种方法）

#### 3、取出文件ett.txt 的第30到40行的内容。

##### 注：ett.txt由seq 20 120&gt;ett.txt创建

#### 4、描述linux的启动/运行级别有几种及其含义。 

#### 5、查找/oldboy目录下所有7天以前的，以log结尾的，并且大于1M的文件，把这些文件复制到/tmp下.	（不少于3种方法） 

#### 6、列出linux下面常用的打包工具并写出相应的压缩解压参数。至少1种

#### 7、如何查看是否开启80端口，及查看sshd进程是否存在？

#### 8、请执行命令取出linux中eth0的IP地址（至少2种方法）

#### 9、常用系统文件问答

1\)通过修改文件\(  \),可以设定开机时自动挂载文件系统。

2\)在linux系统中，当LAN（局域网）内没有条件记案例DNS服务器，但又想让局域网内的用户可以使用计算机名互相访问时，应配置（ ）文件（请写全路径） 

3\)linux系统启动加载完成后，内核将启动名为（ ）的程序，这也是引导过程完成后，内核运行的第一个程序。我们可以修改默认的启动级别为（ ），使得系统重启后自动采用命令行模式登录。

#### 10、请详细描述linux系统从打开主机电源到进入登录界面整个过程的流程。

#### 11、如果向磁盘写入数据提示如下错误：No space left on device，通过df -h查看磁盘空间，发现没满，请问可能原因是什么？ 

#### 12、请给出如下格式的date命令 1）显示日期为2011-02-26这种格式 2）打印三天前的日期格式如：2011-02-26 

#### 13、将/etc/目录打包压缩放在/backup目录，并且要求每天备份的文件名不同，请问如何做？（给出打包压缩的命令即可）

#### 14、通过xshell/SecureCRT等软件远程连接服务器，连接不上，请问如何排查？



