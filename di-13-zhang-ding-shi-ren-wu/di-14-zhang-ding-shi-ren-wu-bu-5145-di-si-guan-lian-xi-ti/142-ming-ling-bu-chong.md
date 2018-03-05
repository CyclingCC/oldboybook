#### 1、userdel 删除用户

注释

参数： -r 删除用户及用户家目录

#### 2、groupadd 添加一个用户组

#### 3、usermod 修改用户信息

-u -g -G -s -M -e -c -d -L -U -l（小写字母L）

#### 4、chage 专门修改用户密码信息

参数：

-l（小写字母L）

-E

-M -W -m -I\(大写字母i\)

#### 5、查看用户状态

id 、w、who、last、lastlog

#### 6、uptime 查看系统运行了多久

#### 7、su 切换用户

参数：

-，-l，--login 切换用户并且初始化（修改）环境变量

-c 执行命令

```
[root@oldboyedu-35 ~]# su - -c whoami
root
```

#### 8、fdisk 磁盘分区\(主要用于小于2TB mbr分区表\)

参数：

-l 查看系统中所有磁盘的信息

-u 以扇区的形式进行分区/查看 默认是柱面

-c 禁止的DOS兼容模式

创建n删除d查看p

#### 9、parted 磁盘分区工具\(用户GPT分区表 大于 2TB\)

parted /dev/sdc print

parted /dev/sdc mklaber gpt

parted /dev/sdc mkpart primary 0 100

parted /dev/sdc mkpart primary 100 200

#### 10、mkfs 格式化工具

参数：

-t 指定文件系统类型

mkfs -t ext4  === mkfs.ext4

#### 11、tune2fs 修改文件系统信息

参数：

-i interval 间隔 文件系统检查的间隔

-c count 次数 每挂载多少次之后进行磁盘检查

例子：

```
tune2fs -i -1 -c -1 /dev/sdb1
```

#### 12、fsck 文件系统检查 file system check

参数：

-a auto repair 自动修复遇到的问题

#### 13、dd 创建一个块

解读：

if input file 输入文件 从哪里读取内容

of output file 输出文件 读取内容后方在哪里

bs block size 每一次读多少内容

count 读取多少次

例子：

```
dd if=/dev/zero of=/tmp/swap bs=1M count=128

dd if=/dev/sda of=/tmp/mbr.bin bs=512 count=1
```

#### 14、mkswap 分区或文件变为swap类型

#### 15、swapon 让swap生效 让文件/分区作为swap

参数：

-s 显示swap统计信息

例子：

```
swapon -s /tmp/swap
```

#### 16、swapoff 关闭

例子：

```
swapoff  /dev/sdb1
```

#### 17、du 显示目录/文件占地面积（所占的磁盘空间）

参数：

-s 显示一共多大

-h 人类可读

#### 练习题：

回忆本章节的重要命令及如何使用

