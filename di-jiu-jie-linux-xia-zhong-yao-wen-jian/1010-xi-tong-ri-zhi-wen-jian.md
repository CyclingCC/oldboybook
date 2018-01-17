/var/log/messages

dmseg 命令可以查看系统故障信息（/var/log/dmesg） 依赖于rsyslog服务开启

轮询日志由 /etc/logrotate.conf 和 /etc/logrotate.d/syslog 控制

| /var/log/secure | 记录登入系统存取信息的文件，按周自动轮询，例如pop3,ssh,telnet,ftp等都会记录在此。系统安全的日志文件，依赖于rsyslog服务 |
| :--- | :--- |
| /var/log/messages | 系统默认的日志文件每周自动切割一次 |
| /var/log/wtmp | 记录登录者信息的文件 |
| /var/spool/cron/root | 定时任务配置文件 |
| /proc/cpuinfo | 关于处理器的信息，如类型、厂家、型号和性能等 top看cpu sar |
| /proc/meminfo | 系统内存信息，free -m |
| /proc/devices | 当前运行内核所配置的所有设备清单 |
| /proc/dma | 当前正在使用的DMA通道 |
| /proc/filesystems | 当前运行内核所配置的文件系统 |
| /proc/interrupts | 正在使用的中断，和曾经有多少个中断 |
| /proc/ioports | 当前正在使用的I/O端口 |
| /proc/loadavg | 系统负载平均值信息（系统的繁忙情况，比较准确，但是不够细致系统性能指标），uptime的结果负载值不要超过CPU的核数看负载top uptime |
| /proc/mounts | 设备的挂载信息， df -h类似 |



