
---

# 第1章 变量

### 1.1  环境变量

#### 1.1.1  查看环境变量

\[root@oldboy36 ~\]\# env

HOSTNAME=oldboy36

TERM=linux

SHELL=/bin/bash

HISTSIZE=1000

SSH\_CLIENT=10.0.0.1 51166 22

SSH\_TTY=/dev/pts/0

USER=root

LS\_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:\*.tar=01;31:\*.tgz=01;31:\*.arj=01;31:\*.taz=01;31:\*.lzh=01;31:\*.lzma=01;31:\*.tlz=01;31:\*.txz=01;31:\*.zip=01;31:\*.z=01;31:\*.Z=01;31:\*.dz=01;31:\*.gz=01;31:\*.lz=01;31:\*.xz=01;31:\*.bz2=01;31:\*.tbz=01;31:\*.tbz2=01;31:\*.bz=01;31:\*.tz=01;31:\*.deb=01;31:\*.rpm=01;31:\*.jar=01;31:\*.rar=01;31:\*.ace=01;31:\*.zoo=01;31:\*.cpio=01;31:\*.7z=01;31:\*.rz=01;31:\*.jpg=01;35:\*.jpeg=01;35:\*.gif=01;35:\*.bmp=01;35:\*.pbm=01;35:\*.pgm=01;35:\*.ppm=01;35:\*.tga=01;35:\*.xbm=01;35:\*.xpm=01;35:\*.tif=01;35:\*.tiff=01;35:\*.png=01;35:\*.svg=01;35:\*.svgz=01;35:\*.mng=01;35:\*.pcx=01;35:\*.mov=01;35:\*.mpg=01;35:\*.mpeg=01;35:\*.m2v=01;35:\*.mkv=01;35:\*.ogm=01;35:\*.mp4=01;35:\*.m4v=01;35:\*.mp4v=01;35:\*.vob=01;35:\*.qt=01;35:\*.nuv=01;35:\*.wmv=01;35:\*.asf=01;35:\*.rm=01;35:\*.rmvb=01;35:\*.flc=01;35:\*.avi=01;35:\*.fli=01;35:\*.flv=01;35:\*.gl=01;35:\*.dl=01;35:\*.xcf=01;35:\*.xwd=01;35:\*.yuv=01;35:\*.cgm=01;35:\*.emf=01;35:\*.axv=01;35:\*.anx=01;35:\*.ogv=01;35:\*.ogx=01;35:\*.aac=01;36:\*.au=01;36:\*.flac=01;36:\*.mid=01;36:\*.midi=01;36:\*.mka=01;36:\*.mp3=01;36:\*.mpc=01;36:\*.ogg=01;36:\*.ra=01;36:\*.wav=01;36:\*.axa=01;36:\*.oga=01;36:\*.spx=01;36:\*.xspf=01;36:

MAIL=/var/spool/mail/root

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

PWD=/root

LANG=en\_US.UTF-8

HISTCONTROL=ignoredups

SHLVL=1

HOME=/root

LOGNAME=root

CVS\_RSH=ssh

SSH\_CONNECTION=10.0.0.1 51166 10.0.0.100 22

LESSOPEN=\|\|/usr/bin/lesspipe.sh %s

G\_BROKEN\_FILENAMES=1

\_=/bin/env

#### 1.1.2  查看所有变量

\[root@oldboy36 ~\]\# set

BASH=/bin/bash

BASHOPTS=checkwinsize:cmdhist:expand\_aliases:extquote:force\_fignore:hostcomplete:interactive\_comments:login\_shell:progcomp:promptvars:sourcepath

BASH\_ALIASES=\(\)

BASH\_ARGC=\(\)

BASH\_ARGV=\(\)

BASH\_CMDS=\(\)

BASH\_LINENO=\(\)

BASH\_SOURCE=\(\)

BASH\_VERSINFO=\(\[0\]="4" \[1\]="1" \[2\]="2" \[3\]="2" \[4\]="release" \[5\]="x86\_64-redhat-linux-gnu"\)

BASH\_VERSION='4.1.2\(2\)-release'

COLORS=/etc/DIR\_COLORS

COLUMNS=96

CVS\_RSH=ssh

DIRSTACK=\(\)

EUID=0

GROUPS=\(\)

G\_BROKEN\_FILENAMES=1

HISTCONTROL=ignoredups

HISTFILE=/root/.bash\_history

HISTFILESIZE=1000

HISTSIZE=1000

HOME=/root

HOSTNAME=oldboy36

HOSTTYPE=x86\_64

ID=0

IFS=$' \t\n'

LANG=en\_US.UTF-8

LESSOPEN='\|\|/usr/bin/lesspipe.sh %s'

LINES=29

LOGNAME=root

LS\_COLORS='rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:\*.tar=01;31:\*.tgz=01;31:\*.arj=01;31:\*.taz=01;31:\*.lzh=01;31:\*.lzma=01;31:\*.tlz=01;31:\*.txz=01;31:\*.zip=01;31:\*.z=01;31:\*.Z=01;31:\*.dz=01;31:\*.gz=01;31:\*.lz=01;31:\*.xz=01;31:\*.bz2=01;31:\*.tbz=01;31:\*.tbz2=01;31:\*.bz=01;31:\*.tz=01;31:\*.deb=01;31:\*.rpm=01;31:\*.jar=01;31:\*.rar=01;31:\*.ace=01;31:\*.zoo=01;31:\*.cpio=01;31:\*.7z=01;31:\*.rz=01;31:\*.jpg=01;35:\*.jpeg=01;35:\*.gif=01;35:\*.bmp=01;35:\*.pbm=01;35:\*.pgm=01;35:\*.ppm=01;35:\*.tga=01;35:\*.xbm=01;35:\*.xpm=01;35:\*.tif=01;35:\*.tiff=01;35:\*.png=01;35:\*.svg=01;35:\*.svgz=01;35:\*.mng=01;35:\*.pcx=01;35:\*.mov=01;35:\*.mpg=01;35:\*.mpeg=01;35:\*.m2v=01;35:\*.mkv=01;35:\*.ogm=01;35:\*.mp4=01;35:\*.m4v=01;35:\*.mp4v=01;35:\*.vob=01;35:\*.qt=01;35:\*.nuv=01;35:\*.wmv=01;35:\*.asf=01;35:\*.rm=01;35:\*.rmvb=01;35:\*.flc=01;35:\*.avi=01;35:\*.fli=01;35:\*.flv=01;35:\*.gl=01;35:\*.dl=01;35:\*.xcf=01;35:\*.xwd=01;35:\*.yuv=01;35:\*.cgm=01;35:\*.emf=01;35:\*.axv=01;35:\*.anx=01;35:\*.ogv=01;35:\*.ogx=01;35:\*.aac=01;36:\*.au=01;36:\*.flac=01;36:\*.mid=01;36:\*.midi=01;36:\*.mka=01;36:\*.mp3=01;36:\*.mpc=01;36:\*.ogg=01;36:\*.ra=01;36:\*.wav=01;36:\*.axa=01;36:\*.oga=01;36:\*.spx=01;36:\*.xspf=01;36:'

MACHTYPE=x86\_64-redhat-linux-gnu

MAIL=/var/spool/mail/root

MAILCHECK=60

OPTERR=1

OPTIND=1

OSTYPE=linux-gnu

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin

PIPESTATUS=\(\[0\]="0"\)

PPID=1262

PS1='\[\u@\h \W\]$ '

PS2='&gt; '

PS4='+ '

PWD=/root

SHELL=/bin/bash

SHELLOPTS=braceexpand:emacs:hashall:histexpand:history:interactive-comments:monitor

SHLVL=1

SSH\_CLIENT='10.0.0.1 51166 22'

SSH\_CONNECTION='10.0.0.1 51166 10.0.0.100 22'

SSH\_TTY=/dev/pts/0

TERM=linux

UID=0

USER=root

\_=env

colors=/etc/DIR\_COLORS

### 1.2  PATH环境变量

PATH 环境变量 存放命令的路径/位置

# 第2章 linux命令帮助

linux下面查询帮助

man 命令

命令 --help

help  命令  （linux内置命令）

# 第3章 ls命令的集合

-F   给不同文件加不同符号标示

-p   只给目录加斜线

-t    按修改时间排序

-r    排序时翻转

--color=auto  给不同文件加不同颜色

如何过滤出已知当前目录下 oldboy 中的所有一级目录\(提示:不包含 oldboy 目录下面目录的子目录及隐藏目录，即只能是一级目录\)？

创建环境

mkdir /oldboy -p

cd /oldboy

mkdir ext/oldboy test xiaodong xiaofan xingfujie -p

touch jeacen oldboy wodi.gz yingsui.gz

tree

### 3.1  tree

\[root@oldboy oldboy\]\# tree -dLi 1

.

a

ext

test

xiaodong

xiaofan

xingfujie

### 3.2  find

\[root@oldboy oldboy\]\# find /oldboy/ -maxdepth 1 -type d ! -name "oldboy"

/oldboy/test

/oldboy/ext

/oldboy/xingfujie

/oldboy/a

/oldboy/xiaofan

/oldboy/xiaodong

\[root@oldboy oldboy\]\# find . -maxdepth 1 -type d ! -name "."

./test

./xiaodong

./xiaofan

./xingfujie

./ext

### 3.3  ls

\[root@oldboy36 oldboy\]\# ll -d /oldboy/\*/

drwxr-xr-x 3 root root 4096 May  7 21:52 /oldboy/a/

drwxr-xr-x 3 root root 4096 May 10 10:16 /oldboy/ext/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/test/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xiaodong/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xiaofan/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xingfujie/

### 3.4  ls  grep

\[root@oldboy oldboy\]\# ll /oldboy/ \|grep "^d"

drwxr-xr-x 3 root root 4096 May  7 21:52 a

drwxr-xr-x 3 root root 4096 May 10 10:16 ext

drwxr-xr-x 2 root root 4096 May 10 10:16 test

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaodong

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaofan

drwxr-xr-x 2 root root 4096 May 10 10:16 xingfujie

\[root@oldboy oldboy\]\# ls -lF \|grep "/$"

drwxr-xr-x 3 root root 4096 3月  20 16:03 ext/

drwxr-xr-x 2 root root 4096 3月  20 16:03 test/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaodong/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaofan/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xingfujie/

### 3.5  ls   sed

\[root@oldboy36 oldboy\]\# ll /oldboy/ \|sed -n '/^d/p'

drwxr-xr-x 3 root root 4096 May  7 21:52 a

drwxr-xr-x 3 root root 4096 May 10 10:16 ext

drwxr-xr-x 2 root root 4096 May 10 10:16 test

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaodong

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaofan

drwxr-xr-x 2 root root 4096 May 10 10:16 xingfujie

### 3.6  ls   awk

\[root@oldboy36 oldboy\]\# ll \|awk '$2&gt;1'

total 36

drwxr-xr-x 3 root root 4096 May  7 21:52 a

drwxr-xr-x 3 root root 4096 May 10 10:16 ext

drwxr-xr-x 2 root root 4096 May 10 10:16 test

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaodong

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaofan

drwxr-xr-x 2 root root 4096 May 10 10:16 xingfujie

\[root@oldboy oldboy\]\# ls -l\|awk '/^d/'

drwxr-xr-x 3 root root 4096 3月  20 16:03 ext

drwxr-xr-x 2 root root 4096 3月  20 16:03 test

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaodong

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaofan

drwxr-xr-x 2 root root 4096 3月  20 16:03 xingfujie

\[root@oldboy oldboy\]\# ls -pl \|awk '/\/$/'

drwxr-xr-x 3 root root 4096 3月  20 16:03 ext/

drwxr-xr-x 2 root root 4096 3月  20 16:03 test/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaodong/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xiaofan/

drwxr-xr-x 2 root root 4096 3月  20 16:03 xingfujie/

### 3.7  一个目录中有很多文件（ls -l 查看时好多屏），想用一条命令最快速度查看到最近更新的文件。如何看？

\[root@oldboy36 ~\]\# ls -lrt

total 60

-rw-r--r--. 1 root root  5890 May  1 12:12 install.log.syslog

-rw-r--r--. 1 root root 21736 May  1 12:15 install.log

-rw-------. 1 root root  1303 May  1 12:15 anaconda-ks.cfg

-rw-r--r--  1 root root  2747 May  1 17:18 init.sh

-rw-r--r--  1 root root    18 May  7 11:53 test.txt

drwxr-xr-x  2 root root  4096 May  7 21:26 test

-rw-r--r--  1 root root    18 May  8 18:31 oldboy.txt

-rw-r--r--  1 root root   324 May  8 18:55 ett.txt

# 第4章  cd

假如当前目录是如下命令的结果：

\[root@oldboy oldboy\]\# pwd    \#==&gt;这是打印当前目录的，最菜的命令了，你该会的。

/oldboy

现在因为需要进入到了/tmp 目录下进行操作，执行的命令如下：

\[root@oldboy oldboy\]\# cd /tmp

\[root@oldboy tmp\]\# pwd

/tmp

操作完毕后，希望快速返回上一次进入的目录，即/oldboy 目录，该如何做呢？（提示：不能用 cd /oldboy 命令呦）

cd  -

cd  .

cd  ..   切换到上级目录

cd  -   切换到上一次所在目录

cd  ~   切换到家目录

cd      切换到家目录

cd  ~oldboy  切换到oldboy家目录

### 第5章 find

-maxdepth 1  查找深度

\[root@oldboy36 oldboy\]\# find /oldboy/ -maxdepth 1 -type d ! -name "oldboy"

/oldboy/test

/oldboy/ext

/oldboy/xingfujie

/oldboy/a

/oldboy/xiaofan

/oldboy/xiaodong

已知 apache 服务的访问日志按天记录在服务器本地目录/app/logs 下，由于磁盘空间紧张，现在要求只能保留最近 7 天的访问日志！请问如何解决？ 请给出解决办法或配置或处理命令。（提示：可以从 apache 服务配置上着手，也可以从生成出来的日志上着手。）

创建环境

touch -d "20170501" access\_www\_2017-04-{01..10}.log

touch -d "20170504" access\_www\_2017-04-{11..20}.log

touch -d "20170508" access\_www\_2017-04-{21..30}.log

mkdir /app/logs -p

cd /app/logs

for n in \`seq 20\`

do

date -s "2016/03/$n"

touch access\_www\_\`\(date +%F\)\`.log

done

date -s "2016/03/20 17:05"

\[root@oldboy36 logs\]\# find /app/logs/ -type f -name "\*.log" -mtime +7 \|xargs ls -l

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-01.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-02.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-03.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-04.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-05.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-06.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-07.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-08.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-09.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-10.log

\[root@oldboy36 logs\]\# find /app/logs/ -type f -name "\*.log" -mtime +7 -exec ls -l {} \;

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-09.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-01.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-08.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-06.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-04.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-07.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-02.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-05.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-10.log

-rw-r--r-- 1 root root 0 May  1 00:00 /app/logs/access\_www\_2017-04-03.log

find /app/logs/ -type f -name "acc\*.log" -mtime +7\|xargs rm -f

find /app/logs/ -type f -name "acc\*.log" -mtime +7 -exec rm {} \;

rm -f \`find /app/logs/ -type f -name "acc\*.log" -mtime +7\`

[http://oldboy.blog.51cto.com/2561410/1750481](http://oldboy.blog.51cto.com/2561410/1750481)

# 第6章 tree

-L  层数

-d  目录

\[root@oldboy36 oldboy\]\# tree -dL 1

.

├── a

├── ext

├── test

├── xiaodong

├── xiaofan

└── xingfujie

\[root@oldboy36 oldboy\]\# tree -dLi 1

.

a

ext

test

xiaodong

xiaofan

xingfujie

# 第7章 grep

-i 不区分大小写

-n  对匹配的内容显示行号

--color=auto

\[root@oldboy logs\]\# grep -n "." nginx.conf

1:stu01

2:stu02

3:stu03

4:stu04

5:stu05

6:stu06

7:stu07

8:stu08

9:stu09

10:stu10

11:stu11

12:stu12

13:stu13

14:stu14

15:stu15

16:stu16

17:stu17

18:stu18

19:stu19

20:stu20

\[root@oldgirl oldboy\]\# grep "oldboy" /etc/hosts

10.33.33.129  www.baidu.com oldboy

\[root@oldgirl oldboy\]\# grep --color=auto "oldboy" /etc/hosts

10.33.33.129  www.baidu.com oldboy

\[root@oldgirl oldboy\]\# echo "alias grep='grep --color=auto'" &gt;&gt;/etc/profile

\[root@oldgirl oldboy\]\# tail -1 /etc/profile

alias grep='grep --color=auto'

\[root@oldgirl oldboy\]\# . /etc/profile

welcome to oldboy linux training from /etc/profile.d

\[root@oldgirl oldboy\]\# grep --color=auto"oldboy" /etc/hosts

# 第8章 nl 命令

显示行号，不包括空行

\[root@oldboy logs\]\# nl nginx.conf

```
 1  stu01

 2  stu02

 3  stu03

 4  stu04

 5  stu05

 6  stu06

 7  stu07

 8  stu08

 9  stu09

10  stu10

11  stu11

12  stu12

13  stu13

14  stu14

15  stu15

16  stu16

17  stu17

18  stu18

19  stu19

20  stu20
```

# 第9章 tail

-f   跟踪文件尾部的变化

-F   比f多了retry功能

tailf  相当于 tail -f

调试系统服务时，希望能实时查看/var/log/messages 系统日志的更新,如何做？

tail -f /var/log/messages

tailf /var/log/messages

# 第10章 cat

\[root@oldboy logs\]\# echo stu{01..20}\|xargs -n1 &gt;nginx.conf

\[root@oldboy logs\]\# cat nginx.conf

stu01

stu02

stu03

stu04

stu05

stu06

stu07

stu08

stu09

stu10

stu11

stu12

stu13

stu14

stu15

stu16

stu17

stu18

stu19

stu20

\[root@oldboy logs\]\# cat -n nginx.conf

```
 1  stu01

 2  stu02

 3  stu03

 4  stu04

 5  stu05

 6  stu06

 7  stu07

 8  stu08

 9  stu09

10  stu10

11  stu11

12  stu12

13  stu13

14  stu14

15  stu15

16  stu16

17  stu17

18  stu18

19  stu19

20  stu20
```

# 第11章 less

\[root@oldboy logs\]\# less -N nginx.conf

```
  1 stu01

  2 stu02

  3 stu03

  4 stu04

  5 stu05

  6 stu06

  7 stu07

  8 stu08

  9 stu09

 10 stu10

 11 stu11

 12 stu12

 13 stu13

 14 stu14

 15 stu15

 16 stu16

 17 stu17

 18 stu18

 19 stu19

 20 stu20
```

# 第12章  awk  sed   grep

12.1  grep

\[root@oldboy36 oldboy\]\# grep -n "." nginx.conf

1:stu01

2:stu02

3:stu03

4:stu04

5:stu05

6:stu06

7:stu07

8:stu08

9:stu09

10:stu10

11:stu11

12:stu12

13:stu13

14:stu14

15:stu15

16:stu16

17:stu17

18:stu18

19:stu19

20:stu20

12.2  awk

\[root@oldboy logs\]\# awk '{print NR,$0}' nginx.conf

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

12.3  sed

\[root@oldboy36 oldboy\]\# sed = nginx.conf \|xargs -n2

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

\[root@oldboy36 oldboy\]\# sed = nginx.conf \| sed 'N;s\#\n\# \#'

1 stu01

2 stu02

3 stu03

4 stu04

5 stu05

6 stu06

7 stu07

8 stu08

9 stu09

10 stu10

11 stu11

12 stu12

13 stu13

14 stu14

15 stu15

16 stu16

17 stu17

18 stu18

19 stu19

20 stu20

# 第13章  打印轻量级 web 服务的配置文件 nginx.conf 内容的行号及内容，该如何做？

nl nginx.conf（不记录空行行号）

cat -n nginx.conf  &lt;==这个最常用。

less -N nginx.conf

vi/vim 文件 然后执行:set nu，:set nonu为取消行号。

grep -n "."  /etc/services 对过滤的内容显示行号，想对所有文件显示行号，就得过滤所有内容。“.”表示任意单个字符。

awk '{print NR,$0}' messages  \#NR表示行号，$0表示整行内容。

sed = oldboy.log\| sed 'N;s/\n/ /'

# 第14章  vim 帮助

:help G

# 第15章  linux系统启动

### 15.1  linux 系统运行级别一般为 0-6，请分别写出每个级别的含义

#### 15.1.1  运行级别

0 - 停止

1 - 单用户模式

2 - 多用户，无NFS

3 - 完全多用户模式

4 - 未使用

5 - X11（图形模式）

6 - 重新启动

#### 15.1.2  系统运行级别配置文件

/etc/inittab

id:3:initdefault:

#### 15.1.3  查看运行级别

\[root@oldboy36 oldboy\]\# runlevel

N 3

#### 15.1.4  切换运行级别

\[root@oldboy36 oldboy\]\# init 2

\[root@oldboy36 oldboy\]\# runlevel

3 2

# 第16章 软件开机启动

### 16.1  装完 Centos 系统后，希望网络文件共享服务 NFS，仅在 3 级别上开机自启动，该如何做？

chkconfig --level 3 iptables on

chkconfig iptables on

### 16.2  查看iptables开机启动状态

\[root@oldboy36 oldboy\]\# chkconfig --list iptables

iptables        0:off   1:off   2:off   3:off   4:off   5:off   6:off

\[root@oldboy36 oldboy\]\# chkconfig \|grep iptables

iptables        0:off   1:off   2:off   3:off   4:off   5:off   6:off

# 第17章  系统字符集

linux 系统中查看中文乱码，请问如何解决乱码问题？

\[root@oldboy36 oldboy\]\# echo $LANG

en\_US.UTF-8

\[root@oldboy36 oldboy\]\# cat /etc/sysconfig/i18n

LANG="en\_US.UTF-8"

SYSFONT="latarcyrheb-sun16"

##### 查看系统支持的字符集

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

# 第18章  文件归档

18.1  /etc/目录为 linux 系统的默认的配置文件及服务启动命令的目录

a.请用 tar 打包/etc 整个目录（打包及压缩）

b.请用 tar 打包/etc 整个目录（打包及压缩，但需要排除/etc/services 文件）

c.请把 a 命令的压缩包，解压到/tmp 指定目录下（最好只用 tar 命令实现）

tar  为文件和目录创建档案

tar命令格式：

tar   \(选项\)\(参数\)  归档文件   \[文件或目录\]

参数    参数说明    其他说明

-z    gzip压缩格式

-c    创建归档

-f    指定归档文件

-r    给归档文件中添加文件

-t    列出归档文件的内容

-x    从归档中提取文件

-v    显示执行过程

-C  &lt;目录&gt;    指定解压到的目录

--exclude=文件目录    排除文件    --exclude=/etc/services   --exclude=c --exclude=b

-h    需要打包的文件是软链接用此参数

-P    从/开始打包

tar zcf /root/etc-pc.tar.gz etc/ --exclude=etc/services

tar xf etc.tar.gz -C /tmp/

# 第19章 练习题

##### 已知如下命令及结果：

\[oldboy@test ~\]$ echo "I am oldboy,myqq is 31333741"&gt;&gt;oldboy.txt

\[oldboy@test ~\]$ cat oldboy.txt

I am oldboy,myqq is 31333741

##### 现在需要从文件中过滤出“oldboy”和“31333741”字符串，请给出命令

##### 创建环境

mkdir /oldboy

echo "I am oldboy,myqq is 31333741"&gt;/oldboy/oldboy.txt

\[root@oldboy36 oldboy\]\# cd /oldboy/

\[root@oldboy36 oldboy\]\# cat oldboy.txt

I am oldboy,myqq is 31333741

##### 19.1 方法1  sed+sed

\[root@oldboy36 oldboy\]\# sed 's\#I am \#\#' oldboy.txt \|sed 's\#,myqq is\#\#'

oldboy 31333741

##### 19.2  方法2  cut+sed

\[root@oldboy36 oldboy\]\# cut -d " " -f3,5 oldboy.txt \|sed 's\#,myqq\#\#'

oldboy 31333741

\[root@oldboy36 oldboy\]\# sed 's\#,\# \#' oldboy.txt \|cut -d ' ' -f3,6

oldboy 31333741

##### 19.3  方法3  awk+sed

\[root@oldboy36 oldboy\]\# awk '{print $3,$5}' oldboy.txt \|sed 's\#,myqq\#\#'

oldboy 31333741

\[root@oldboy36 oldboy\]\# sed 's\#,\# \#' oldboy.txt \|awk '{print $3,$6}'

oldboy 31333741

##### 19.4  方法4  awk

\[root@oldboy36 oldboy\]\# awk -F "\[, \]" '{print $3,$6}' oldboy.txt

oldboy 31333741

\[root@oldboy36 oldboy\]\# awk -F "\[, \]" '{print $3,$NF}' oldboy.txt

oldboy 31333741

\[root@oldboy36 oldboy\]\# awk -F "\[ ,\]" '{print $3","$6}' oldboy.txt

oldboy,31333741

##### 19.5  方法5  cut

\[root@oldboy36 oldboy\]\# cut -c6-11,20- oldboy.txt

oldboy 31333741

# 第20章  wc  统计数量

### 20.1   如何查看/etc/services 文件内容有多少行？

\[root@oldboy36 oldboy\]\# wc -l /etc/services

10774 /etc/services

\[root@oldboy36 oldboy\]\# grep -n . /etc/services \|tail -1

10774:iqobject        48619/udp               \# iqobject

# 第21章

### 21.1  过滤出/etc/services  文件包含 3306 或 1521 两数据库端口的行的内容

\[root@oldboy36 oldboy\]\# egrep "3306\|1521" /etc/services

mysql           3306/tcp                        \# MySQL

mysql           3306/udp                        \# MySQL

ncube-lm        1521/tcp                \# nCube License Manager

ncube-lm        1521/udp                \# nCube License Manager

\[root@oldboy36 oldboy\]\# grep "3306\\|1521" /etc/services

mysql           3306/tcp                        \# MySQL

mysql           3306/udp                        \# MySQL

ncube-lm        1521/tcp                \# nCube License Manager

ncube-lm        1521/udp                \# nCube License Manager

# 第22章  特殊符号

单引号：所见即所得，吃啥吐啥

双引号：解析特殊符号,输出解析后的结果：例如:$LANG

不加引号：和双引号类似，但是支持通配符  \*

### 22.1 引号和不加引号的区别1：

\[root@oldboytx ~\]\# touch a b

\[root@oldboytx ~\]\# ll

total 0

-rw-r--r--. 1 root root 0 Jun 25 16:25 a

-rw-r--r--. 1 root root 0 Jun 25 16:25 b

\[root@oldboytx ~\]\# touch "a b"

\[root@oldboytx ~\]\# ll

total 0

-rw-r--r--. 1 root root 0 Jun 25 16:25 a

-rw-r--r--. 1 root root 0 Jun 25 16:25 a b

-rw-r--r--. 1 root root 0 Jun 25 16:25 b

### 22.2 引号和不加引号的区别2：

\[root@oldboy36 tmp\]\# ll

总用量 0

-rw-r--r-- 1 root root 0 6月  25 19:36 ?

-rw-r--r-- 1 root root 0 6月  25 19:32 \*

-rw-r--r-- 1 root root 0 6月  25 19:33 aa

-rw-r--r-- 1 root root 0 6月  25 19:33 abc

-rw-r--r-- 1 root root 0 6月  25 19:33 b

\[root@oldboy36 tmp\]\# ll ?

-rw-r--r-- 1 root root 0 6月  25 19:36 ?

-rw-r--r-- 1 root root 0 6月  25 19:32 \*

-rw-r--r-- 1 root root 0 6月  25 19:33 b

\[root@oldboy36 tmp\]\# ll "?"

-rw-r--r-- 1 root root 0 6月  25 19:36 ?

\[root@oldboy36 tmp\]\# ll \*

-rw-r--r-- 1 root root 0 6月  25 19:36 ?

-rw-r--r-- 1 root root 0 6月  25 19:32 \*

-rw-r--r-- 1 root root 0 6月  25 19:33 aa

-rw-r--r-- 1 root root 0 6月  25 19:33 abc

-rw-r--r-- 1 root root 0 6月  25 19:33 b

\[root@oldboy36 tmp\]\# ll "\*"

-rw-r--r-- 1 root root 0 6月  25 19:32 \*

### 22.3 双引号和单引号区别1：

关于$

\[root@oldboytx ~\]\# echo "$LANG"

en\_US.UTF-8

\[root@oldboytx ~\]\# echo '$LANG'

$LANG

### 22.4 双引号和单引号区别2：

关于\`\`

\[root@oldboytx ~\]\# echo "\`which awk\`"

/bin/awk

\[root@oldboytx ~\]\# echo '\`which awk\`'

\`which awk\`

### 22.5 双引号和单引号区别3：

#### 关于 !

\[root@oldboytx ~\]\# echo '!ll'

!ll

\[root@oldboytx ~\]\# echo "!ll"

echo "ll /bin/awk "

ll /bin/awk

\#通配符    {}  \*  \[\]  ?

