### 一、linux 系统中查看中文乱码，请问如何解决乱码问题？

#### 1、查看字符集

\[root@oldboy36 oldboy\]\# echo $LANG

en\_US.UTF-8

\[root@oldboy36 oldboy\]\# cat /etc/sysconfig/i18n

LANG="en\_US.UTF-8"

SYSFONT="latarcyrheb-sun16"

#### 2、查看系统支持的字符集

\[root@iZ2570yi9c2Z ~\]\# locale -a

aa\_DJ

aa\_DJ.iso88591

aa\_DJ.utf8

aa\_ER

aa\_ER@saaho

aa\_ER.utf8

aa\_ER.utf8@saaho

aa\_ET

aa\_ET.utf8

af\_ZA

............

\[root@iZ2570yi9c2Z ~\]\# locale

LANG=en\_US.UTF-8

LC\_CTYPE="en\_US.UTF-8"

LC\_NUMERIC="en\_US.UTF-8"

LC\_TIME="en\_US.UTF-8"

LC\_COLLATE="en\_US.UTF-8"

LC\_MONETARY="en\_US.UTF-8"

LC\_MESSAGES="en\_US.UTF-8"

LC\_PAPER="en\_US.UTF-8"

LC\_NAME="en\_US.UTF-8"

LC\_ADDRESS="en\_US.UTF-8"

LC\_TELEPHONE="en\_US.UTF-8"

LC\_MEASUREMENT="en\_US.UTF-8"

LC\_IDENTIFICATION="en\_US.UTF-8"

LC\_ALL=

#### 3、字符集的介绍

Linux中文显示设置（如何防止显示中文乱码）

此项优化为可选项，即调整Linux系统的字符集设置，那么，什么是字符集呢？

简单说，字符集就是一套文字符号及其编码。目前linux下常用的字符集有：

i、GBK：定长，双字节，不是国际标准，支持的系统不少，实际企业用的不多

ii、UTF-8：非定长，1-4字节，广泛支持，MYSQL也使用UTF-8，企业广泛应用

可通过跨级的命令方式在/etc/sysconfig/i18n中添加如下内容，使其支持中文显示：

\[root@oldboyedu44 ~\]\# echo $LANG

en\_US.UTF-8

\[root@oldboyedu44 ~\]\# cat /etc/sysconfig/i18n 

LANG="en\_US.UTF-8"

SYSFONT="latarcyrheb-sun16"

\[root@oldboyedu44 sysconfig\]\# cp /etc/sysconfig/i18n{,.bak}  ===&gt;备份

\[root@oldboyedu44 sysconfig\]\# echo 'LANG="zh\_CN.UTF-8"' &gt;/etc/sysconfig/i18n ===&gt;修改配置文件

#### 4、中文乱码的解决方案

字符集 标识文字符号的方法

UTF-8  万国码 Linux默认字符集

GBK

##### 为何出现乱码？

远程连接工具（xshell）字符集  与 系统的字符集不同

##### 第1个里程碑-查看系统使用的字符集

\#LANG环境变量-存放的是系统的字符集和语音

\[root@oldboyedu42 ~\]\# $LANG

-bash: en\_US.UTF-8: command not found

\[root@oldboyedu42 ~\]\# echo $LANG

en\_US.UTF-8

\#语言.字符集

##### 第2个里程碑-修改字符集-临时-重新登陆后

\[root@oldboyedu42 ~\]\# export LANG=zh\_CN.UTF-8

\[root@oldboyedu42 ~\]\# echo $LANG

zh\_CN.UTF-8

##### 第3个里程碑-永久生效

\[root@oldboyedu42 ~\]\# cat  /etc/sysconfig/i18n 

LANG="en\_US.UTF-8"

SYSFONT="latarcyrheb-sun16"

\[root@oldboyedu42 ~\]\# source   /etc/sysconfig/i18n

