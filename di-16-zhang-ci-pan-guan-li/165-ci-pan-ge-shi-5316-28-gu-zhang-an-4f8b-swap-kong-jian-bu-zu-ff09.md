#### 1、磁盘格式化

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

8193

正在写入inode表: 完成

Creating journal \(1024 blocks\): 完成

Writing superblocks and filesystem accounting information: 完成

This filesystem will be automatically checked every 31 mounts or

180 days, whichever comes first. Use tune2fs -c or -i to override.

\[root@oldboy ~\]\# tune2fs -c -1 /dev/sdc1 取消文件系统自动检查

tune2fs 1.41.12 \(17-May-2010\)

Setting maximal mount count to -1

#### 2、partprobe /dev/sdc 报错

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

#### 3、xfs分区格式：

yum install xfsprogs kmod-xfs xorg-x11-xfs xfsdump -y

mkfs.xfs -f /dev/sdb1

#### 4、挂载

\[root@oldboy ~\]\# mount /dev/sdc1 /mnt/

\[root@oldboy ~\]\# df -h

Filesystem Size Used Avail Use% Mounted on

/dev/sda3 7.7G 1.5G 5.8G 20% /

tmpfs 495M 0 495M 0% /dev/shm

/dev/sda1 190M 36M 145M 20% /boot

/dev/sdc1 9.7M 100K 9.0M 2% /mnt

#### 5、硬盘被分区后格式化过程

硬盘被分区后，真正的格式化过程：

1）格式化

mkfs.ext4 /dev/sdb1

mkfs -t ext3 /dev/sdb1

mkfs -t ext3 -b 4096 -I 512 /dev/sdb1

查看格式化后的文件系统信息dumpe2fs命令。

2）取消文件系统自动检查（可选）

tune2fs -c -1 /dev/sdb1

3）挂载（临时挂载）

mount -o rw,sync /dev/sdb1 /mnt

4）查看挂载情况，及参数信息

df -h

cat /proc/mounts

5）开机自动挂载

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

#### 6、对损坏的磁盘做手动检查

方法1：

fsck -C -f -t ext4 /dev/sdb1

方法2：

\[root@oldboy ~\]\# badblocks -sv /dev/sdb1

Checking blocks 0 to 20479

Checking for bad blocks \(read-only test\): done

Pass completed, 0 bad blocks found.

#### 7、如何检查并修复/dev/hda5

fsck -C -t msdos -a /dev/hda5

e2fsck -p /dev/hda5

#### 作业：fstab被破坏了，导致系统无法启动，如何修复？

使用光盘引导进入救援模式，或者在单用户模式下，使用mount / -o remount 重新挂载提权，然后修改/etc/fstab文件，修改正确后重启即可

#### 8、parted 分区

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

起始扇区（可以不写）

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

## 9、fdisk parted ext4 xfs {#222--fdisk--parted--ext4--xfs}

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

#### 10、故障案例-swap空间不足

日常运维工作过程中，我们经常会遇到swap空间不足的情况，甚至nagios都把swap监控作为一个基础的系统监控项，足以看出这个性能指标的重要性。

一般是MySQL数据库机器比较容易发生swap空间不足，也有应用服务器高负载的情况下也会产生这现象。

##### 为什么会产生swap使用呢？

假设我们的物理内存是32G，swap是4G。如果MySQL本身已经占用了24G物理内存，

而同时其他程序或者系统模块又需要8G内存，这时候操作系统就可能把MySQL所拥有的一部分地址空间映射到swap上去。 

比如拷贝或压缩一个大文件，或用mysqldump导出一个很大的数据库的时候，文件系统往往会向Linux申请大量的内存作为cache，

一不小心就会导致L使用swap。这个情景比较常见，以下是最简单的三个调整方法：

① /proc/sys/vm/swappiness的内容改成0（临时），/etc/sysctl.conf上添加vm.swappiness=0（永久）

这个参数决定了Linux是倾向于使用swap，还是倾向于释放文件系统cache。在内存紧张的情况下，数值越低越倾向于释放文件系统cache。当然，这个参数只能减少使用swap的概率，并不能避免Linux使用swap。

② 修改MySQL的配置参数innodb\_flush\_method，开启O\_DIRECT模式。这种情况下，InnoDB的buffer pool会直接绕过文件系统cache来访问磁盘，但是redo log依旧会使用文件系统cache。值得注意的是，Redo log是覆写模式的，即使使用了文件系统的cache，也不会占用太多。

③ 添加MySQL的配置参数memlock，这个参数会强迫mysqld进程的地址空间一直被锁定在物理内存上，对于os来说是非常霸道的一个要求。必须要用root帐号来启动MySQL才能生效。还有一个比较复杂的方法，指定MySQL使用大页内存（Large Page）。Linux上的大页内存是不会被换出物理内存的，和memlock有异曲同工之妙。

程序运行的一个必要条件就是足够的内存，而内存往往是系统里面比较紧张的一种资源。为了满足更多程序的要求，操作系统虚拟了一部分内存地址，

并将之映射到 swap上。对于程序来说，它只知道操作系统给自己分配了内存地址，但并不清楚这些内存地址到底映射到物理内存还是swap。

物理内存和swap在功能上是一样的，只是因为物理存储元件的不同（内存和磁盘），性能上有很大的差别。操作系统会根据程序使用内存的特点

进行换入和换出，尽可能地把物理内存留给最需要它的程序。但是这种调度是 按照预先设定的某种规则的，并不能完全符合程序的需要。



