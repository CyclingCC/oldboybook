### 一、分区总览

![](https://www.luffycity.com/linux-book/assets/23-23.png)

#### 1、MBR

mbr是磁盘上的一小段扇区, 用来存放代码的空间

grub是一段引导程序

![](https://www.luffycity.com/linux-book/assets/23-24.png)

#### 2、16B分区表

![](https://www.luffycity.com/linux-book/assets/tab23-29.png)

#### 3、分区类型

msdos

gpt

#### 4、导出磁盘MBR信息

dd if=/dev/sda of=mbr.bin bs=512 count=1

\[root@c71 ~\]\# od -xa /tmp/mbr.bin

0000000 4658 4253 0000 0010 0000 0000 0100 002c

X   F   S   B nul nul dle nul nul nul nul nul nul soh   , nul

0000020 0000 0000 0000 0000 0000 0000 0000 0000

nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul

0000040 3fb1 c2f7 777a 0f4b 1eaf c0ea ce8e fb96

1   ?   w   B   z   w   K  si   /  rs   j   @  so   N syn   {

0000060 0000 0000 0100 0400 0000 0000 0000 8000

nul nul nul nul nul soh nul eot nul nul nul nul nul nul nul nul

0000100 0000 0000 0000 8100 0000 0000 0000 8200

nul nul nul nul nul nul nul soh nul nul nul nul nul nul nul stx

0000120 0000 0100 0000 004b 0000 0400 0000 0000

nul nul nul soh nul nul   K nul nul nul nul eot nul nul nul nul

0000140 0000 5503 b4b4 0002 0001 1000 0000 0000

nul nul etx   U   4   4 stx nul soh nul nul dle nul nul nul nul

0000160 0000 0000 0000 0000 090c 0408 000f 1900

nul nul nul nul nul nul nul nul  ff  ht  bs eot  si nul nul  em

0000200 0000 0000 0000 0002 0000 0000 0000 b700

nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul   7

0000220 0000 0000 0000 00cc 0000 0000 0000 0000

nul nul nul nul nul nul   L nul nul nul nul nul nul nul nul nul

0000240 ffff ffff ffff ffff ffff ffff ffff ffff

del del del del del del del del del del del del del del del del

0000260 0000 0000 0000 0200 0000 0000 0000 0000

nul nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul

0000300 0000 0000 0000 0100 0000 8a00 0000 8a00

nul nul nul nul nul nul nul soh nul nul nul  nl nul nul nul  nl

0000320 0000 0000 0000 0000 0000 0000 0000 0000

nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul

\*

0001000

#### 5、 磁盘分区重点：

1、给磁盘分区的实质就是针对0磁头0磁道1扇区的前446B后面接下来的64B的分区表进行设置

主要是划分起始以及结束磁头号、扇区号及柱面号

2、给磁盘分区的工具有fdisk（适合给小于2T的磁盘分区），parted（擅长给大于2T的磁盘分区，

可以对小于2T的磁盘分区），首选fdisk，只有大于2T 时才去选parted

##### 企业面试题： 一台服务器6块600G的磁盘，raid5后，总大小3T，此时无法装系统，为什么？ {#企业面试题：-一台服务器6块600g的磁盘，raid5后，总大小3t，此时无法装系统，为什么？}

解决：

方法1： 做raid5 后，不要重启装系统，在raid界面，继续分一个小的虚拟磁盘vd 200G，用这个

200G的虚拟磁盘装系统，装完系统后再把剩余的2.8T分区通过parted

方法2： 先拿一块盘raid0，剩余5块在做raid5，在raid0装系统

方法3： 装系统时，选下gpt分区格式，即可安装系统

3、 一块磁盘的分区表仅有64B大小，每个分区表占用16B，因此一块磁盘仅支持四个分区表信息

主分区+扩展分区的总量不超过4个

4、磁盘分区是按照柱面（cylinder）来划分的

5、扩展分区不能直接使用，还需要在扩展分区的基础上创建逻辑分区才行

6、扩展分区有自己的分区表，因此，扩展分区下面的逻辑分区可以有多个

磁盘在使用前一般需要进行分区，当然如果不分区直接格式化使用也是没有问题的，但这不是常见的

磁盘分区（主分区、扩展分区和逻辑分区之分。一块硬盘最多可以有4个分区表信息（磁盘本身限制）），

其中一个主分区的位置可以用一个扩展分区替换，且一块硬盘只能有一个扩展分区（操作系统限制），

在这个扩展分区内可以划分多个逻辑分区

#### 6、主分区 primary

一般来说，主分区是磁盘上必须存在的分区，一般为磁盘的第一个分区，我们可以在这个分区

上安装操作系统

/boot 主分区

swap 主分区

/ 主分区

#### 7、 扩展分区 extended

扩展分区不能算一个正常的分区，而是一个链接，起到一个指向的作用，我们可以再扩展分区内

建立逻辑分区，扩展分区就像一个虚拟出来的一个小硬盘

一块硬盘只能存在一个扩展分区，并且扩展分区不能直接存放数据

#### 8、 逻辑分区 logical

逻辑分区必须存在于扩展分区内，在扩展分区可以划分多个逻辑分区，逻辑分区的编号从

5开始

实际应用：主分区和逻辑分区，都可以使用，一般系统安装用主分区，存放数据都可以

#### 9、磁盘分区的几个问题范例

1、如果我要将我的一块大磁盘暂时分成四个分区，同时，还希望有其他的空间可以让我

在未来需要的时候再进行分区

3p+1e（1L）剩余空间保留

2p+1e （2L）剩余空间保留

1p+1e（3L） 剩余空间保留

2、假如我有一块SAS硬盘，我想要把磁盘分成6个分区，那么每个磁盘分区在linux系统下

的数字遍号是多少？

1p+1E /dev/sda1, /dev/sda5……

2p+1E /dev/sda1,/dev/sda2, /dev/sda5……

3p+1E /dev/sda1, /dev/sda2, /dev/sda3, /dev/sda5……

生产场景不同角色linux服务器分区案例

[http://oldboy.blog.51cto.com/2561410/634725](http://oldboy.blog.51cto.com/2561410/634725)

[http://oldboy.blog.51cto.com/2561410/629558](http://oldboy.blog.51cto.com/2561410/629558)

#### 10、磁盘分区的设备名称

设备名称的定义规则如下，其他的分区可以依次类推：

第一块IDE接口磁盘 /dev/hda

第二块IDE接口磁盘 /dev/hdb

第一块SCSI接口磁盘 /dev/sda

第二块SCSI接口磁盘 /dev/sdb

SATA SAS 都是 sd开头

每个分区则使用磁盘名称加对应的数字编号表示：

第一块IDE接口磁盘的第1个分区 /dev/hda1

第一块IDE接口磁盘的第5个分区 /dev/hda5

第二块SCSI接口磁盘的第1个分区 /dev/sdb1

第二块SCSI接口磁盘的第5个分区 /dev/sdb5

#### 11、fdisk分区

\[root@oldboy ~\]\# fdisk /dev/sdc

WARNING: DOS-compatible mode is deprecated. It's strongly recommended to

switch off the mode \\\(command 'c'\\\) and change display units to

sectors \\\(command 'u'\\\).

Command \(m for help\): m

Command action

a toggle a bootable flag

b edit bsd disklabel

c toggle the dos compatibility flag

d delete a partition 删除一个分区

l list known partition types 查看分区类型对应编号列表

m print this menu 打印帮助菜单

n add a new partition 新建一个分区

o create a new empty DOS partition table

p print the partition table 打印分区表

q quit without saving changes 退出程序，不保存

s create a new empty Sun disklabel

t change a partition's system id 更改分区类型

u change display/entry units

v verify the partition table

w write table to disk and exit 将操作写入分区表并退出程序

x extra functionality \(experts only\)

Command \(m for help\): n

Command action

e extended

p primary partition \(1-4\)

p

Partition number \(1-4\): 1

First cylinder \(1-102, default 1\):

Using default value 1

Last cylinder, +cylinders or +size{K,M,G} \(1-102, default 102\): +10M

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

Command \(m for help\): n

Command action

e extended

p primary partition \(1-4\)

p

Partition number \(1-4\): 2

First cylinder \(12-102, default 12\):

Using default value 12

Last cylinder, +cylinders or +size{K,M,G} \(12-102, default 102\): +10M

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

Command \(m for help\): n

Command action

e extended

p primary partition \(1-4\)

p

Partition number \(1-4\): 3

First cylinder \(23-102, default 23\):

Using default value 23

Last cylinder, +cylinders or +size{K,M,G} \(23-102, default 102\): +10M

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

/dev/sdc3 23 33 11264 83 Linux

Command \(m for help\): n

Command action

e extended

p primary partition \(1-4\)

e

Selected partition 4

First cylinder \(34-102, default 34\):

Using default value 34

Last cylinder, +cylinders or +size{K,M,G} \(34-102, default 102\):

Using default value 102

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

/dev/sdc3 23 33 11264 83 Linux

/dev/sdc4 34 102 70656 5 Extended

Command \(m for help\): n

First cylinder \(34-102, default 34\):

Using default value 34

Last cylinder, +cylinders or +size{K,M,G} \(34-102, default 102\): +10M

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

/dev/sdc3 23 33 11264 83 Linux

/dev/sdc4 34 102 70656 5 Extended

/dev/sdc5 34 44 11248 83 Linux

Command \(m for help\): n

First cylinder \(45-102, default 45\):

Using default value 45

Last cylinder, +cylinders or +size{K,M,G} \(45-102, default 102\):

Using default value 102

Command \(m for help\): p

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

/dev/sdc3 23 33 11264 83 Linux

/dev/sdc4 34 102 70656 5 Extended

/dev/sdc5 34 44 11248 83 Linux

/dev/sdc6 45 102 59376 83 Linux

Command \(m for help\): w

The partition table has been altered!

Calling ioctl\(\) to re-read partition table.

Syncing disks.

##### fdisk -cu /dev/sdb {#fdisk--cu-devsdb}

#### 12、查看磁盘分区

\[root@oldboy ~\]\# fdisk -l

Disk /dev/sda: 10.7 GB, 10737418240 bytes

255 heads, 63 sectors/track, 1305 cylinders

Units = cylinders of 16065 \* 512 = 8225280 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0x00044026

Device Boot Start End Blocks Id System

/dev/sda1 \* 1 26 204800 83 Linux

Partition 1 does not end on cylinder boundary.

/dev/sda2 26 281 2048000 82 Linux swap / Solaris

Partition 2 does not end on cylinder boundary.

/dev/sda3 281 1306 8231936 83 Linux

Disk /dev/sdb: 1073 MB, 1073741824 bytes

255 heads, 63 sectors/track, 130 cylinders

Units = cylinders of 16065 \* 512 = 8225280 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0x00000000

Disk /dev/sdc: 106 MB, 106954752 bytes

64 heads, 32 sectors/track, 102 cylinders

Units = cylinders of 2048 \* 512 = 1048576 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0xaf6251f5

Device Boot Start End Blocks Id System

/dev/sdc1 1 11 11248 83 Linux

/dev/sdc2 12 22 11264 83 Linux

/dev/sdc3 23 33 11264 83 Linux

/dev/sdc4 34 102 70656 5 Extended

/dev/sdc5 34 44 11248 83 Linux

/dev/sdc6 45 102 59376 83 Linux

#### 13、查看磁盘分区UUID

\[root@oldboy36 ~\]\# blkid

/dev/sda1: UUID="4c40caf4-8676-4b30-9cd3-9ecdbaa79acd" TYPE="ext4"

/dev/sda2: UUID="5eaa6bea-ffdc-477b-ae6c-94a7fe20838f" TYPE="swap"

/dev/sda3: UUID="70c86ea3-354e-45e3-a2d8-186ecbbc7292" TYPE="ext4"

#### 



