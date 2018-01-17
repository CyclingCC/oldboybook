# 分区 {#第2章-分区}

![](https://www.luffycity.com/linux-book/assets/23-23.png)

## 2.1 MBR {#21--mbr}

mbr是磁盘上的一小段扇区, 用来存放代码的空间

grub是一段引导程序

![](https://www.luffycity.com/linux-book/assets/23-24.png)

## 2.2 16B分区表 {#22---16b分区表}

![](https://www.luffycity.com/linux-book/assets/tab23-29.png)

## 2.3 分区类型 {#23--分区类型}

msdos

gpt

## 2.4 导出磁盘MBR信息 {#24--导出磁盘mbr信息}

dd if=/dev/sda of=mbr.bin bs=512 count=1

\[root@c71 ~\]\# od -xa /tmp/mbr.bin

0000000 4658 4253 0000 0010 0000 0000 0100 002c

```
  X   F   S   B nul nul dle nul nul nul nul nul nul soh   , nul

```

0000020 0000 0000 0000 0000 0000 0000 0000 0000

```
nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul

```

0000040 3fb1 c2f7 777a 0f4b 1eaf c0ea ce8e fb96

```
  1   ?   w   B   z   w   K  si   /  rs   j   @  so   N syn   {

```

0000060 0000 0000 0100 0400 0000 0000 0000 8000

```
nul nul nul nul nul soh nul eot nul nul nul nul nul nul nul nul

```

0000100 0000 0000 0000 8100 0000 0000 0000 8200

```
nul nul nul nul nul nul nul soh nul nul nul nul nul nul nul stx

```

0000120 0000 0100 0000 004b 0000 0400 0000 0000

```
nul nul nul soh nul nul   K nul nul nul nul eot nul nul nul nul

```

0000140 0000 5503 b4b4 0002 0001 1000 0000 0000

```
nul nul etx   U   4   4 stx nul soh nul nul dle nul nul nul nul

```

0000160 0000 0000 0000 0000 090c 0408 000f 1900

```
nul nul nul nul nul nul nul nul  ff  ht  bs eot  si nul nul  em

```

0000200 0000 0000 0000 0002 0000 0000 0000 b700

```
nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul   7

```

0000220 0000 0000 0000 00cc 0000 0000 0000 0000

```
nul nul nul nul nul nul   L nul nul nul nul nul nul nul nul nul

```

0000240 ffff ffff ffff ffff ffff ffff ffff ffff

```
del del del del del del del del del del del del del del del del

```

0000260 0000 0000 0000 0200 0000 0000 0000 0000

```
nul nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul

```

0000300 0000 0000 0000 0100 0000 8a00 0000 8a00

```
nul nul nul nul nul nul nul soh nul nul nul  nl nul nul nul  nl

```

0000320 0000 0000 0000 0000 0000 0000 0000 0000

```
nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul

```

\*

0001000

## 2.5 磁盘分区重点： {#25--磁盘分区重点：}

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

## 2.6 主分区 primary {#26--主分区-primary}

一般来说，主分区是磁盘上必须存在的分区，一般为磁盘的第一个分区，我们可以在这个分区

上安装操作系统

/boot 主分区

swap 主分区

/ 主分区

## 2.7 扩展分区 extended {#27--扩展分区-extended}

扩展分区不能算一个正常的分区，而是一个链接，起到一个指向的作用，我们可以再扩展分区内

建立逻辑分区，扩展分区就像一个虚拟出来的一个小硬盘

一块硬盘只能存在一个扩展分区，并且扩展分区不能直接存放数据

## 2.8 逻辑分区 logical {#28--逻辑分区-logical}

逻辑分区必须存在于扩展分区内，在扩展分区可以划分多个逻辑分区，逻辑分区的编号从

5开始

实际应用：主分区和逻辑分区，都可以使用，一般系统安装用主分区，存放数据都可以

## 2.9 磁盘分区的几个问题范例 {#29---磁盘分区的几个问题范例}

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

## 2.10 磁盘分区的设备名称 {#210--磁盘分区的设备名称}

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

## 2.11 fdisk分区 {#211--fdisk分区}

\[root@oldboy ~\]\# fdisk /dev/sdc

WARNING: DOS-compatible mode is deprecated. It's strongly recommended to

```
 switch off the mode \\(command 'c'\\) and change display units to

 sectors \\(command 'u'\\).

```

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

## 2.12 查看磁盘分区 {#212-查看磁盘分区}

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

## 2.13 查看磁盘分区UUID {#213--查看磁盘分区uuid}

\[root@oldboy36 ~\]\# blkid

/dev/sda1: UUID="4c40caf4-8676-4b30-9cd3-9ecdbaa79acd" TYPE="ext4"

/dev/sda2: UUID="5eaa6bea-ffdc-477b-ae6c-94a7fe20838f" TYPE="swap"

/dev/sda3: UUID="70c86ea3-354e-45e3-a2d8-186ecbbc7292" TYPE="ext4"

## 2.14 格式化 {#214-格式化}

\[root@oldboy ~\]\# partprobe /dev/sdc 强制内核重新查找一次分区表 （分区完成后执行此命令）

\[root@oldboy ~\]\# mkfs.ext4 /dev/sdc1

mke2fs 1.41.12 \(17-May-2010\)

文件系统标签=

操作系统:Linux

块大小=1024 \(log=0\)

分块大小=1024 \(log=0\)

Stride=0 blocks, Stripe width=0 blocks

2816 inodes, 11248 blocks

562 blocks \(5.00%\) reserved for the super user

第一个数据块=1

Maximum filesystem blocks=11534336

2 block groups

8192 blocks per group, 8192 fragments per group

1408 inodes per group

Superblock backups stored on blocks:

```
8193

```

正在写入inode表: 完成

Creating journal \(1024 blocks\): 完成

Writing superblocks and filesystem accounting information: 完成

This filesystem will be automatically checked every 31 mounts or

180 days, whichever comes first. Use tune2fs -c or -i to override.

\[root@oldboy ~\]\# tune2fs -c -1 /dev/sdc1 取消文件系统自动检查

tune2fs 1.41.12 \(17-May-2010\)

Setting maximal mount count to -1

## 2.15 partprobe /dev/sdc 报错 {#215---partprobe-devsdc-报错}

Warning: WARNING: the kernel failed to re-read the partition table on /dev/sdb \(Device or resource busy\). As a result, it may not reflect all of your changes until after reboot

解决方法：

1、重启机器可以解决

2、 lsof /dev/sdb 看一下是否有程式在使用中，如果有可以杀掉进程试试

mkfs.ext4 -b 4096 -I 256 /dev/sdb1

tune2fs -c 0 -i 0 /dev/sdb1

\[root@oldboy ~\]\# dumpe2fs /dev/sdb1 \|egrep -i "\(inode\|block\) size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size: 4096

Inode size: 256

## 2.16 xfs分区格式： {#216-xfs分区格式：}

yum install xfsprogs kmod-xfs xorg-x11-xfs xfsdump -y

mkfs.xfs -f /dev/sdb1

## 2.17 挂载 {#217-挂载}

\[root@oldboy ~\]\# mount /dev/sdc1 /mnt/

\[root@oldboy ~\]\# df -h

Filesystem Size Used Avail Use% Mounted on

/dev/sda3 7.7G 1.5G 5.8G 20% /

tmpfs 495M 0 495M 0% /dev/shm

/dev/sda1 190M 36M 145M 20% /boot

/dev/sdc1 9.7M 100K 9.0M 2% /mnt

## 2.18 硬盘被分区后格式化过程 {#218--硬盘被分区后格式化过程}

硬盘被分区后，真正的格式化过程：

1、格式化

mkfs.ext4 /dev/sdb1

mkfs -t ext3 /dev/sdb1

mkfs -t ext3 -b 4096 -I 512 /dev/sdb1

查看格式化后的文件系统信息dumpe2fs命令。

2、取消文件系统自动检查（可选）

tune2fs -c -1 /dev/sdb1

3、挂载（临时挂载）

mount -o rw,sync /dev/sdb1 /mnt

4、查看挂载情况，及参数信息

df -h

cat /proc/mounts

5、开机自动挂载

把mount /dev/sdb1 /mnt 放入/etc/rc.local，适合网络文件系统，NFS,MFS,GFS。

按照fstab的格式加入上述挂载信息。/etc/fstab，适合本地磁盘。

要挂载的设备 挂载点 挂载类型 挂载选项 备份 磁盘检查

UUID=4bc27c91-8cae-44fb-ba19-4213d1d47326 /mnt ext4 defaults 0 0

/dev/sdb2 /opt ext3 defaults 0 0

要挂载的设备可以是设备路径，也可以是对应的UUID。

特别注意：执行mount -a测试挂载，否则开机可能导致系统起不来。

\[root@c66-mobban1 ~\]\# blkid

/dev/sda1: UUID="88020ecf-caae-4f70-abd5-f01890594ebe" TYPE="ext4"

/dev/sda2: UUID="d3a79fb3-e573-4380-a2f9-2ffa0edaca79" TYPE="swap"

/dev/sda3: UUID="1dd4d340-204d-4ce1-b7b2-e1cefc61f466" TYPE="ext4"

/dev/sdb1: UUID="4bc27c91-8cae-44fb-ba19-4213d1d47326" TYPE="ext4"

/dev/sdb2: UUID="c8e8b094-166b-40ae-9155-ac29da06c80e" SEC\_TYPE="ext2" TYPE="ext3"

\[root@c66-mobban1 ~\]\# tail -2 /etc/fstab

UUID=4bc27c91-8cae-44fb-ba19-4213d1d47326 /mnt ext4 defaults 0 0

/dev/sdb2 /opt ext3 defaults 0 0

## 2.19 对损坏的磁盘做手动检查 {#219--对损坏的磁盘做手动检查}

方法1：

fsck -C -f -t ext4 /dev/sdb1

方法2：

\[root@oldboy ~\]\# badblocks -sv /dev/sdb1

Checking blocks 0 to 20479

Checking for bad blocks \(read-only test\): done

Pass completed, 0 bad blocks found.

## 2.20 如何检查并修复/dev/hda5 {#220--如何检查并修复devhda5}

fsck -C -t msdos -a /dev/hda5

e2fsck -p /dev/hda5

## 作业：fstab被破坏了，导致系统无法启动，如何修复？ {#作业：fstab被破坏了，导致系统无法启动，如何修复？}

使用光盘引导进入救援模式，或者在单用户模式下，使用mount / -o remount 重新挂载提权，然后修改/etc/fstab文件，修改正确后重启即可

## 2.21 parted 分区 {#221-parted--分区}

不写单位默认为MB

实验：100M盘

parted /dev/sdb mklabel gpt Yes

parted /dev/sdb mkpart primary 0 10 Ignore

parted /dev/sdb mkpart primary linux-swap 11 21 Ignore

parted /dev/sdb mkpart logical ext4 22 32 Ignore

parted /dev/sdb p

parted /dev/sdb rm 3

fdisk 非交互式分区：

parted /dev/sdb mklabel bsd yes 将硬盘分区表由gpt格式转换为bsd格式（MBR）

vi fdisk.txt

n 新建一个分区

p primary分区

1 分区编号

```
    起始扇区（可以不写）

```

+100M 结束扇区 （可以直接写大小）

p 打印分区表

w 保存修改并退出

fdisk /dev/sdb &lt; fdisk.txt 执行分区

ll /dev/sdb\* 检查分区是否成功

mkfs.ext4 /dev/sdb1 格式化分区

mount /dev/sdb1 /mnt 挂载分区

df -h \|grep /dev/sdb1

echo -e "n\np\n1\n\n+10M\nn\np\n2\n\n+10M\nw" \|fdisk /dev/sdb

partprobe

注意： parted 的操作都是实时的，千万不能在生产环境中测试

实验：100M盘

parted /dev/sdb mklabel gpt Yes

parted /dev/sdb mkpart primary 0 10 Ignore

parted /dev/sdb mkpart primary linux-swap 11 21 Ignore

parted /dev/sdb mkpart logical ext4 22 32 Ignore

parted /dev/sdb p

## 2.22 fdisk parted ext4 xfs {#222--fdisk--parted--ext4--xfs}

传统的fdisk分区不支持2T以上的磁盘分区，而parted分区可以支持，而ext4格式不支持16T以上的磁盘空间分区，必须使用xfs分区

2TB以上磁盘分区、制作文件系统：

分为两个主分区\(先创建磁盘标签mklable ，再创建分区mkpart分区类型\)

\[root@localhost ~\]\# parted /dev/sdb \# 使用parted来对GPT磁盘操作，进入交互式模式

\(parted\) mklabel gpt \# 将MBR磁盘格式化为GPT

\(parted\) print \#打印当前分区

\(parted\) mkpart primary 0 4.5TB \# 分一个4.5T的主分区

\(parted\) mkpart primary 4.5TB 12TB \# 分一个7.5T的主分区

\(parted\) print \#打印当前分区

\(parted\) quit 退出

Information: Don’t forget to update /etc/fstab, if necessary.

~~~~~~

通过parted工具来删除分区

\[root@jetsen ~\]\# parted /dev/sde

GNU Parted 1.8.1

Using /dev/sde

Welcome to GNU Parted! Type 'help' to view a list of commands.

（parted） p

Model: VMware, VMware Virtual S （scsi）

Disk /dev/sde: 2190GB

Sector size （logical/physical）： 512B/512B

Partition Table: gpt

Number Start End Size File system Name Flags

1 17.4kB 2190GB 2190GB gpt2t

（parted） rm 1 ----删除1号分区

（parted） p ----显示分区信息，看如下是没有分区的

Model: VMware, VMware Virtual S （scsi）

Disk /dev/sde: 2190GB

Sector size （logical/physical）： 512B/512B

Partition Table: gpt

Number Start End Size File system Name Flags

（parted） q

Information: Don't forget to update /etc/fstab, if necessary.

