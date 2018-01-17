#### 当从root用户切到普通用户时，执行ifconfig会提示

\[oldboy@student ~\]$ ifconfig -bash: ifconfig: command not found

提示：c58会遇到，c64没有此问题。 请问这是为什么？如何解决，请给出详细解决过程

PATH 环境变量中没有ifconfig命令的路径

\[root@xdz ~\]\# which ifconfig

/sbin/ifconfig

echo ' PATH=$ PATH: /sbin/ifconfig ' &gt;&gt; ~/.bash\_profile

. ~/.bash\_profile

