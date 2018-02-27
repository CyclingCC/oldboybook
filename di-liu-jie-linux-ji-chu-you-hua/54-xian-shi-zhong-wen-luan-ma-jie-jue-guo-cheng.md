#### 1、linux 系统中查看中文乱码，请问如何解决乱码问题？

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

