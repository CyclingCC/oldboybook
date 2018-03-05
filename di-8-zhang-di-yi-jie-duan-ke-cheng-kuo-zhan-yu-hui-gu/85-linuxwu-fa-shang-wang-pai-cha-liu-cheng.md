#### 1、验证一下 是否能上网

\[root@oldboyedu42 ~\]\# ping  www.baidu.com

ping: unknown host www.baidu.com

\#unknown host 未知的域名

#### 2、验证 DNS 是否有故障?

\#ping 公网ip地址

此时用ping DNS 是通着的，那么就说明DNS的配置问题

如果还是不通，那么就是虚拟机的配置出问题了

\[root@oldboyedu42 ~\]\# ping  223.5.5.5

PING 223.5.5.5 \(223.5.5.5\) 56\(84\) bytes of data.

64 bytes from 223.5.5.5: icmp\_seq=1 ttl=128 time=32.3 ms

64 bytes from 223.5.5.5: icmp\_seq=2 ttl=128 time=32.9 ms

64 bytes from 223.5.5.5: icmp\_seq=3 ttl=128 time=32.4 ms

64 bytes from 223.5.5.5: icmp\_seq=4 ttl=128 time=32.7 ms

64 bytes from 223.5.5.5: icmp\_seq=5 ttl=128 time=32.9 ms

#### 3、小结

1.IPADDR-ONBOOT-BOOTPROTO-GATEWAY-DNS1-DNS2

2.DNS作用-域名解析为IP地址

3.DNS服务器地址

\#1.阿里云

223.5.5.5

223.6.6.6

\#2.

114.114.114.114

114.114.115.115

4.Linux无法上网的排查过程（屌丝逃离洗浴中心之路）

1）检查是否能上网

ping www.baidu.com

2）检查DNS是否有问题

ping 223.5.5.5

5.修改DNS-重启网卡

#### 练习题：

linux无法上网的排查过程及解决方法

