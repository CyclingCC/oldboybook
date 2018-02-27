#### 1、看路是否通畅

ping 服务器的ip地址（windows\)

命令：ip显示网络信息

ip address === ip a 显示网卡信息

ip address show eth0 ===ip a s eth0  显示某块网卡的信息	

#### 2、是否有人打劫

  防火墙和selinux是否关闭

#### 3、查看是否有人提供服务

服务器的22端口是否开启

windows：

1\#telnet 10.0.0.200 22 

Linux：

ss  -lntup  \#显示系统中已经开启的端口 

ss -lntup \|grep 22

nmap -p22 10.0.0.200

命令：ss   服务器网络连接

-lntup 显示已经开启的端口

命令：nmap 网络扫描命令

-p 22  查看某台机器上面某个端口是否开启 

