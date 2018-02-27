#### Linux开机启动的服务

#### 1.开机 BIOS 自检

#### 2.MBR 引导

#### 硬盘 0 柱面 0 磁道 1 扇区的前 446byte。

#### 3.grub 引导菜单

#### cat /etc/grub.conf

#### 4.加载内核 kernel

#### 5.启动 init 进程

#### \[root@oldboy oldboy\]\# ps -ef\|grep init

#### root 1 0 0 Apr17 ? 00:00:01 init \[3\]

#### 6.读取 inittab 文件，执行 rc.sysinit,rc 等脚本

#### /etc/inittab

#### /etc/rc.d/rc.sysinit

#### /etc/rc.d/rc3.d/ &lt;==文本模式

#### 7.启动 mingetty，进入系统登陆界

#### ![](/assets/4-2.png)

#### 

### 

### 

### 

### 



