/var目录是变量文件——在正常运行的系统中其内容不断变化的文件（动态的程序数据），如日志，脱机文件和临时电子邮件文件。

该目录的内容是经常变动的，/var下有/var/log目录用来存放系统日志的目录。/var/www目录用来定义Apache服务器站点存放目录。/var/lib用来存放一些库文件。

| 重要子目录 | 功能 |
| :--- | :--- |
| /usr/lib | /usr/bin/和/usr/sbin/中二进制文件的库。 |
| /usr/local | 一般编译软件的时候默认路径\(如,yum或rpm安装包默认路径\) |
| /usr/bin | 用户可执行文件目录 |
| /usr/sbin | 非必要的系统二进制文件，例如：大量网络服务的守护进程。 |
| /usr/share | 存放系统共用的东西，如帮助文件 |
| /usr/src | 源码程序存放目录1.rpm –ivh包名.rpm2.yum install包名3.源码\(./configure,make,make install\)定制 |
| /usr/include | 存放C/C++头文件的目录 |

#### /var/adm

比如软件包安装信息、日志、管理信息等就存放在该目录下，在Slackware操作系统中是有这个目录的。在Fedora中好象没有。

#### /var/log

该目录用于存放系统日志。

#### /var/spool

打印机、邮件、代理服务器等假脱机目录存放在该目录下。

