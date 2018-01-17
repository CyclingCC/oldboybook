#### 如何快速查到ifconfig的全路径（假如你不知道其路径），请给出命令

which

\[root@oldboy36 ~\]\# which ifconfig

/sbin/ifconfig

locate

\[root@oldboy36 ~\]\# locate ifconfig

/sbin/ifconfig

/usr/sbin/pifconfig

/usr/share/man/de/man8/ifconfig.8.gz

/usr/share/man/fr/man8/ifconfig.8.gz

/usr/share/man/man8/ifconfig.8.gz

/usr/share/man/man8/pifconfig.8.gz

/usr/share/man/pt/man8/ifconfig.8.gz

whereis

\[root@oldboy36 ~\]\# whereis ifconfig

ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz

find查找

\[root@oldboy36 ~\]\# find /sbin/ /usr/sbin/ /usr/local/sbin/ -type f -name "ifconfig"

/sbin/ifconfig

