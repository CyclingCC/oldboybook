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

