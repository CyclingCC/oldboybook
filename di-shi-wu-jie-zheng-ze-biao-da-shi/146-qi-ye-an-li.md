#### 空行的处理

egrep -v "^$" /oldboy/test.txt

sed '/^$/d' /oldboy/test.txt

awk '/^$/' /oldboy/test.txt

awk '!/^$/' /oldboy/test.txt

#### 企业案例

\[root@oldboy oldboy\]\# find /root/oldboy -type f\|xargs sed -i '/&lt;script language=javascript src=http:\/\/%4%66E%78%6F%72%67%2E%70%6F\/x.js?google\_ad=93x28\_ad&gt;&lt;\/script&gt;/d'

\[root@oldboy oldboy\]\# find /root/oldboy -type f\|xargs sed -i 's\#&lt;script language=javascript src=[http://%4%66E%78%6F%72%67%2E%70%6F/x.js?google\_ad=93x28\_ad&gt;&lt;/script&gt;\#\#g](http://%4fexorg.po/x.js?google_ad=93x28_ad></script>##g)'

#### 取出/etc/passwd中的第一列

egrep -o "^\[a-zA-Z0-9\]+" /etc/passwd

egrep -o "^\[^:\]+" /etc/passwd

sed -r 's\#\(^\[a-zA-Z0-9\#\]+\).\*$\#\1\#g' /etc/passwd

sed -r 's\#\(^\[^:\]+\).\*$\#\1\#g' /etc/passwd

#### 交换/etc/passwd中第一列与最后一列位置

sed -r 's\#\(^\[a-zA-Z0-9\#\]+\)\(:.\*:\)\(.\*$\)\#\3\2\1\#g' /etc/passwd

sed -r 's\#\(^\[^:\]+\)\(:.\*:\)\(.\*$\)\#\3\2\1\#g' /etc/passwd

\[root@oldboy ~\]\# sed -rn 's\#\(^\[^:\]+\)\(:.\*:\)\(.\*\)\#\3\2\1\#gp' /etc/passwd\|head

/bin/bash:x:0:0:root:/root:root

/sbin/nologin:x:1:1:bin:/bin:bin

/sbin/nologin:x:2:2:daemon:/sbin:daemon

/sbin/nologin:x:3:4:adm:/var/adm:adm

/sbin/nologin:x:4:7:lp:/var/spool/lpd:lp

/bin/sync:x:5:0:sync:/sbin:sync

/sbin/shutdown:x:6:0:shutdown:/sbin:shutdown

/sbin/halt:x:7:0:halt:/sbin:halt

/sbin/nologin:x:8:12:mail:/var/spool/mail:mail

/sbin/nologin:x:10:14:uucp:/var/spool/uucp:uucp

