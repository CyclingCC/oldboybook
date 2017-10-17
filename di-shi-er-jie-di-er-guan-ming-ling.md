第1章 变量

1.1  环境变量

1.1.1  查看环境变量

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



1.1.2  查看所有变量

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

PS1='\[\u@\h \W\]\$ '

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



1.2  PATH环境变量

PATH 环境变量 存放命令的路径/位置



第2章 linux命令帮助

linux下面查询帮助

man 命令 

命令 --help 

help  命令  （linux内置命令）



网上搜索

http://linux.51yip.com

http://man.linuxde.net

https://www.linux.org/docs/

https://www.gnu.org/software/coreutils/manual/coreutils.html



第3章 ls  

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





3.1  tree

\[root@oldboy oldboy\]\# tree -dLi 1

.

a

ext

test

xiaodong

xiaofan

xingfujie





3.2  find

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



3.3  ls

\[root@oldboy36 oldboy\]\# ll -d /oldboy/\*/

drwxr-xr-x 3 root root 4096 May  7 21:52 /oldboy/a/

drwxr-xr-x 3 root root 4096 May 10 10:16 /oldboy/ext/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/test/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xiaodong/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xiaofan/

drwxr-xr-x 2 root root 4096 May 10 10:16 /oldboy/xingfujie/



3.4  ls  grep

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



3.5  ls   sed

\[root@oldboy36 oldboy\]\# ll /oldboy/ \|sed -n '/^d/p'

drwxr-xr-x 3 root root 4096 May  7 21:52 a

drwxr-xr-x 3 root root 4096 May 10 10:16 ext

drwxr-xr-x 2 root root 4096 May 10 10:16 test

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaodong

drwxr-xr-x 2 root root 4096 May 10 10:16 xiaofan

drwxr-xr-x 2 root root 4096 May 10 10:16 xingfujie



3.6  ls   awk

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

3.7  一个目录中有很多文件（ls -l 查看时好多屏），想用一条命令最快速度查看到最近更新的文件。如何看？

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

第4章  cd

假如当前目录是如下命令的结果：

\[root@oldboy oldboy\]\# pwd	\#==&gt;这是打印当前目录的，最菜的命令了，你该会的。

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

