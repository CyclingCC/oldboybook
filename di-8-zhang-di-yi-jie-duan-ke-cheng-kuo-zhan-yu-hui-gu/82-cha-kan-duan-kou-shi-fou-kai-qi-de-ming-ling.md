#### 服务器的22端口是否开启

##### 1、windows：

1\#telnet 10.0.0.200 22

##### 2、Linux：

ss  -lntup  \#显示系统中已经开启的端口

ss -lntup \|grep 22

nmap -p22 10.0.0.200



