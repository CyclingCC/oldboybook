#### /etc/目录为 linux 系统的默认的配置文件及服务启动命令的目录

a.请用 tar 打包/etc 整个目录（打包及压缩）

b.请用 tar 打包/etc 整个目录（打包及压缩，但需要排除/etc/services 文件）

c.请把 a 命令的压缩包，解压到/tmp 指定目录下（最好只用 tar 命令实现）

tar 为文件和目录创建档案

tar命令格式：

tar \(选项\)\(参数\) 归档文件 \[文件或目录\]

参数 参数说明 其他说明

-z gzip压缩格式

-c 创建归档

-f 指定归档文件

-r 给归档文件中添加文件

-t 列出归档文件的内容

-x 从归档中提取文件

-v 显示执行过程

-C &lt;目录&gt; 指定解压到的目录

--exclude=文件目录 排除文件 --exclude=/etc/services --exclude=c --exclude=b

-h 需要打包的文件是软链接用此参数

-P 从/开始打包

tar zcf /root/etc-pc.tar.gz etc/ --exclude=etc/services

tar xf etc.tar.gz -C /tmp/

