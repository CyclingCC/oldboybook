### 第一步：看看路是不是通的 {#191-第一步：看看路是不是通的}

ping 服务器：排查客户端到服务器端线路问题，ping是常用的网络连通性检查工具（路通否）

tracert -d 服务器IP：跟踪路由器

路由跟踪命令，也可以检查路由是否通畅，-d 是不对域名进行解析

### 第二步：去服务器端查看 {#192-第二步：去服务器端查看}

service iptables status 和／etc/init.d／iptalbes status这两个命令都可以查看，等效。

linux防火墙iptables，可能好心办坏事，阻挡了远程连接，关掉防火墙，让道路畅通无阻

### 第三步：SSH服务问题 {#193-第三步：ssh服务问题}

telnet + IP地址：查看SSH 22 端口是否打开了（客户端执行）

nmap + IP地址 + -p 22 ：扫描服务器是否开启了22端口

