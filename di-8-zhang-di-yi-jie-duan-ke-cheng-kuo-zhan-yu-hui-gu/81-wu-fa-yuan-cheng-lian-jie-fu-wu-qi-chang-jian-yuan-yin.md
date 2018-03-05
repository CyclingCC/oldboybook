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

#### 4、道路不通常见原因

1\).ip是否正确

2\).网卡是否启动

ip a                == ifconfig

ip address show eth0   ifconfig eth0

ip a s eth0

3\).vmware服务是否启动

win+r ===&gt; services.msc

4\).vmware的配置--&gt;编辑---&gt;虚拟网络编辑器

5\).打开我的电脑/此电脑/计算机  输入"网络连接" 查看vmnet8的配置

#### 练习题：

简述无法远程连接服务的原因

如何解决无法远程连接的服务器？

