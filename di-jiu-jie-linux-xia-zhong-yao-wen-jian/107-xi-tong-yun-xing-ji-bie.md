\[root@oldboy36 ~\]\# cat /etc/inittab

\# inittab is only used by upstart for the default runlevel.

\#

\# ADDING OTHER CONFIGURATION HERE WILL HAVE NO EFFECT ON YOUR SYSTEM.

\#

\# System initialization is started by /etc/init/rcS.conf

\#

\# Individual runlevels are started by /etc/init/rc.conf

\#

\# Ctrl-Alt-Delete is handled by /etc/init/control-alt-delete.conf

\#

\# Terminal gettys are handled by /etc/init/tty.conf and /etc/init/serial.conf,

\# with configuration in /etc/sysconfig/init.

\#

\# For information on how to write upstart event handlers, or how

\# upstart works, see init\(5\), init\(8\), and initctl\(8\).

\#

\# Default runlevel. The runlevels used are:

\# 0 - halt \(Do NOT set initdefault to this\)

\# 1 - Single user mode

\# 2 - Multiuser, without NFS \(The same as 3, if you do not have networking\)

\# 3 - Full multiuser mode

\# 4 - unused

\# 5 - X11

\# 6 - reboot \(Do NOT set initdefault to this\)

\#

id:3:initdefault:

#### 查看当前运行级别

\[root@oldboy36 ~\]\# runlevel

N 3

#### 切换运行级别

\[root@oldboy36 ~\]\# init 2

\[root@oldgirl ~\]\# ll /etc/rc.d/

init.d/ rc0.d/ rc2.d/ rc4.d/ rc6.d/ rc.sysinit

rc rc1.d/ rc3.d/ rc5.d/ rc.local

\[root@oldgirl ~\]\# ll /etc/rc.d/

总用量 60

drwxr-xr-x. 2 root root 4096 3月 6 16:26 init.d

-rwxr-xr-x. 1 root root 2617 7月 24 2015 rc

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc0.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc1.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc2.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc3.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc4.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc5.d

drwxr-xr-x. 2 root root 4096 3月 13 21:02 rc6.d

-rwxr-xr-x. 1 root root 220 7月 24 2015 rc.local

-rwxr-xr-x. 1 root root 20097 7月 24 2015 rc.sysinit

\[root@oldgirl ~\]\# ll /etc/rc.d/rc3.d/

总用量 0

lrwxrwxrwx. 1 root root 16 3月 6 16:26 K01smartd -&gt; ../init.d/smartd

#### 服务管理程序目录 /etc/init.d/

\[root@oldboy36 ~\]\# /etc/init.d/iptables status

iptables: Firewall is not running.

\[root@oldboy36 ~\]\# /etc/init.d/iptables stop

