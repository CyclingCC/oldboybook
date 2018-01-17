如果此时端口已经都正常，但无法连接到服务器上，请查看ssh配置文件中是否禁止了 root用户登录，vi/etc/ssh/sshd\_config 中有相关的 参数 PermitRootLogin 看后面是否更改为了no .默认是yes ,即允许root登陆连接

