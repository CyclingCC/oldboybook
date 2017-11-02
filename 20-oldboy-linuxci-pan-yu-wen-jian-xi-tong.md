# 第1章 磁盘管理

## 1.1 磁盘知识体系结构

![](/assets/23-1.png)

## 1.2  磁盘发展史

IBM350RAMAC 可以说是磁盘的开山鼻祖，它与现代磁盘在外形上的差别很大。现代磁盘的真正原形是1973年IBM公司推出的Winchester（温氏）磁盘，它的特点是：“磁盘在工作时，磁头悬浮在高速转动的磁盘盘片上方，而不与盘片直接接触。磁盘在工作时，磁头沿高速旋转的盘片上方做径向移动”，这便是当今所有磁盘的雏形。现代的磁盘容量虽然更大了，但是依然在沿用“温彻斯特”的动作模式，我们称这种磁盘为机械磁盘

##### 盘片圆周运动，磁头径向运动

![](/assets/tab23-25.png)

## 1.3  磁盘外部结构

![](/assets/23-2.png)

![](/assets/23-3.png)

##### IDE磁盘

![](/assets/23-4.png)

##### SATA接口

![](/assets/23-5.png)

##### pci-e 接口

![](/assets/23-6.png)

##### 正面

![](/assets/23-7.png)

##### 背面

## ![](/assets/23-8.png)

## 1.4  磁盘作用

存放程序和数据

## 1.5  磁盘厂家

西部数据、希捷、三星

## 1.6 磁盘分类

机械（SAS&gt;SATA&gt;IDE）

固态磁盘（Solid State Drive、IDE FLASH DISK）SSD

固态磁盘有两种：

基于闪存（FLASH芯片）的固态磁盘

基于DRAM的固态磁盘

硬盘类型:机械硬盘\(ide  sata  sas  scsi\) 固态硬盘\(sata  pci-e  m.2\)

## 1.7  控制电路板

大多数的控制电路板都采用贴片式焊接，包括主轴调速电路、磁头驱动与伺服定位电路、读写电路、控制与接口电路等。在电路板上还有一块ROM芯片，里面固化的程序可以进行磁盘的初始化，执行加电和启动主轴电机，加电初始寻道、定位以及故障检测等。在电路板上还安装有容量不等的高速数据缓存芯片（计算机世界缓存无处不在）

SLC（Single Layer Cell 单层单元）和 MLC（Multi-Level Cell 多层单元）。SLC的特点是成本高、容量小、但是速度快，而MLC的特点是容量大成本低，但是速度慢。MLC的每个单元是2bit的，相对于SLC来说整整多了一倍。不过，由于每个MLC存储单元中存放的资料较多，结构相对复杂，出错的几率会增加，必须进行错误修正，这个动作导致其性能大幅落后于结构简单的SLC闪存。此外，SLC闪存的优点是复写次数高达100000次，比MLC闪存高10倍。此外，为了保证MLC的寿命，控制芯片都校验和智能磨损平衡技术算法，使得每个存储单元的写入次数可以平均分摊，达到100万小时故障时隔时间（MTBF）

![](/assets/23-9.png)

## 1.8 缓存和缓冲

1、linux系统的特性是将系统不用的物理内存作为缓存区和缓冲区使用

2、buffer为写入缓冲区，sync将缓冲区数据写入磁盘

3、cache为读取数据的缓存区

4、机械磁盘读写都太慢了，所以都使用缓冲和缓存技术

5、门户网站都会用缓存技术，让用户写入读取尽可能不接触磁盘，或者说把用户的请求尽可能往前推

## 1.9  光纤通道

光纤通道（Fibre Channel）和SCSI接口一样光纤通道最初也不是为磁盘设计开发的接口技术，是专门为网络系统设计的，但随着存储系统对速度的需求，才逐渐应用到磁盘系统中。

光纤通道磁盘是为提高多磁盘存储系统的速度和灵活性才开发的，它的出现大大提高了多磁盘系统的通信速度。光纤通道的主要特性有：热插拔性、高速带宽、远程连接、连接设备数量大等

光纤通道是为在像服务器这样的多磁盘系统环境而设计，能满足高端工作站、服务器、海量存储子网络、外设间通过集线器、交换机和点对点连接进行双向、串行数据通讯等系统对高数据传输率的要求

## 1.10  生产工作中服务器选型

DELL，HP,IBM等，其中DELL，HP是互联网公司的主流服务器，这两个品牌的服务器综合的性价比比较高。百度很多用IBM的服务器

## 1.11  企业生产工作中磁盘选型

当前服务器市场：主流磁盘为SAS、SATA、SSD磁盘

### 1.11.1  企业级SAS硬盘（默认）

企业里常见的SAS硬盘是15000转/分。当前主流300G、600G、1000G，从具体的业务需求及性价比考虑，工作中多用300-600G的SAS硬盘

一般选6\_300G  6\_600G  单盘容量不要太大，除非纯备份

用途：用于提供生产线上（工作环境 线上环境）的普通对外提供服务的业务服务器

例如：生产线上的数据库业务、存储业务、图片业务及相关高并发业务（web http，cache服务），

总的来说，如果没有特殊业务需求，SAS磁盘是生产环境首选的磁盘配置

### 1.11.2  企业级SATA硬盘

企业级SATA硬盘，7200-10000转/分，常见的容量为1T和2T，4T，6T， 优点是经济实惠容量大，从具体的业务需求及性价比考虑，在工作中多用SATA磁盘做线下不提供服务的数据存储或者并发业务访问不是很大的业务应用，比如站点程序及数据库、图片的线下备份等

特性：容量性价比高，一般2T的SATA磁盘比较好

磁盘选购小结：

1）线上的业务，用SAS磁盘。

2）线下的业务，用SATA磁盘，磁带库。

3）线上高并发、小容量（很多人都想看的图片）的业务，SSD磁盘。

4）成本思想：根据数据的访问热度，智能分析分层存储。SATA+SSD

[http://oldboy.blog.51cto.com/2561410/926983/](http://oldboy.blog.51cto.com/2561410/926983/)

## 1.12 各种类型磁盘比较

![](/assets/tab23-26.png)

## 1.13 企业案例

1、极端方法-用于门户非核心 1、快 2、可能丢数据

![](/assets/23-10.png)

门户极端案例：高并发，大数据，会把数据写到内存，然后再定时或者定量写到磁盘，

最终还是会加载到内存

特点：a、高并发的写入性能高  b、可能会丢失一部分在内存中还没有来得及存入磁盘的数据

2、常规方法：用于中小企业  1、低性能 2、data不丢

![](/assets/23-11.png)

## 1.14 磁盘内部结构

磁盘的内部结构主要包括：盘片、磁头、盘片主轴、控制电机、磁头控制器、数据转换器、接口、缓存等几个部分。所有的盘片都固定在一个旋转轴上，这个轴及盘片主轴。而所有的盘片之间是平行的，在每个盘片（一个盘片两个盘面）的每个存储面上都有一个磁头，磁头与盘片之间的距离比头发丝的直径还小很多倍。所有的磁头（一个有效盘面就有一个磁头）连在一个磁头控制器上，由磁头控制器负责各个磁头的运动。磁头可沿盘片的半径方向做径向运动（就是沿着半径由圆心到圆周线做直线运动），而盘片以每分钟数千转的速度在高速旋转，这样磁头就能对盘片上的指定位置进行数据的读写。磁盘是非常精密的设备，震动、灰尘等是磁盘损坏的重要原因，所以磁盘需要密封，并且防止剧烈震动。

![](/assets/23-12.png)

![](/assets/23-13.png)

![](/assets/23-14.jpg)

![](/assets/23-15.png)

![](/assets/23-16.png)

![](/assets/23-17.png)

### 1.14.1 磁头组件

![](/assets/23-18.png)

### 1.14.2 磁头驱动

寻道是移动磁头

磁盘读取数据的工作原理是利用特定的磁粒子的极性来记录数据。磁头在读取数据时，

将磁粒子的不同极性转换成不同的电脉冲信号，再利用数据转换器将这些原始信号变成

电脑可以使用的数据，写的操作正好与此相反

### 1.14.3 磁盘片

盘片是磁盘存储数据的真正载体，磁盘盘片大多采用金属薄膜材料

磁盘主轴的转数是衡量磁盘读写性能的重要参数之一

磁盘的每个盘片的每个有效盘面都会有一个读写磁头（磁头数=盘片个数\*2）

“0”磁道非常重要，系统的引导程序就在0磁头0磁道1扇区的前446Byte

### 1.14.4 磁盘的盘面

磁盘的每一个盘片都有两个盘面，一般来说，每个盘面都可以存储数据，成为

有效盘面

### 1.14.5 磁盘的磁道

磁盘在格式化时被分成许多同心圆，同心圆的轨迹就是磁道

磁道由盘面从外向内依次从0开始顺序编号

磁盘的每一个盘面一般都有300~1024 个磁道

### 1.14.6 磁盘的扇区

操作系统是以扇区为单位将信息存储在磁盘上的，一般情况下每个扇区大小为512B

三维地址：磁头（盘片）、磁道（柱面号）、扇区号

### 1.14.7  磁道柱面扇区总结

1、一块磁盘有2-14个盘片，每个盘片有两个面，每个面对应一个读写磁头，

用磁盘头号来区分盘面，即盘面数就是磁头数，盘片数\*2=磁头数（盘面数）

2、不同盘面的磁道被划分为多个扇区，每个区域就是一个扇区（Sector）

3、同一个盘面，以盘片中心为圆心，每个不同半径的圆形轨迹就是一个 磁道（Track）

4、不同盘面相同半径的磁道组成一个圆柱面就是柱面（Cylinder）

5、一个柱面包含多个磁道（这些磁道半径相同），一个磁道包含多个扇区

6、数据信息记录可表示为：某磁头、某（磁道）柱面、某扇区

磁道：每个盘片有两个面，都可记录信息。盘片表面以盘片中心为圆心，用于记录数据的不同半径的

圆形磁化轨迹为磁道。磁化轨迹是磁化区域，看不见

扇区：盘面由圆心向四周画直线，不同的磁道被直线分成许多扇形的区域，

每个弧形区域叫做扇区，每个扇区大小一般为512B

柱面：磁盘中，不同的盘片（或盘面）相同半径的磁道轨迹从上到下组成的圆柱形

### 1.14.8  磁盘相关名词

![](/assets/tab23-27.png)

## 1.15 磁盘接口类型

IDE、SATA、SCSI、光纤通道

IDE  早期的家用，淘汰

SCSI 早期的服务器领域

SATA 流行的家用领域

SAS   流行的服务器领域

FC    高端服务器

## 1.16  SSD固态硬盘接口类型

1、SATA接口：SATA  SATA2  SATA3.0

2、PATA（IDE接口）：IDE44PIN  IDE40PIN

3、PCI-E 接口：mSATA  m.2\(ngff\)  PCIE\(IDE\)  PCIE\(SATA\)ZIF:ZIF接口等

## 1.17 选磁盘

企业生产环境主流磁盘的相关信息对比：

企业生产场景普及程度：SAS&gt;SATA&gt;SSD

单位容量对比性能和价格：SSD&gt;SAS&gt;SATA（一块SSD和一块SATA）

单位价格购买磁盘容量：SATA&gt;SAS&gt;SSD

SSD固态磁盘主流接口类型分为：

1）SATA接口：SATA SATA2 SATA3.0

2）PATA（IDE接口）：IDE44PIN IDE40PIN

3）PCI-E接口：mSATA PCIE\(IDE\) PCIE\(SATA\)ZIF:ZIF接口等

重要优势：随机存取速度，功耗，防震，重量方面优势很大，特别是存取性能。

重要缺点：容量、价格、写寿命，数据恢复难。

采购磁盘

1、主轴转数：5400/7200/10000/15000RPM

2、接口：sata/sas/scsi/ide/pci-e

3、读写更灵敏的磁头

SSD固态磁盘与传统机械磁盘优劣势对比



1.18 企业生产工作中磁盘选型

1、当前服务器市场：主流磁盘为SAS、SATA、SSD

企业级SAS方案（默认）：

企业里常见的SAS硬盘是15000转/分（这里是主轴的转数）当前主流300G、600G、1000G，

从具体的业务需求及性价比考虑，老男孩老师在工作中多用300-600G的SAS硬盘

一般选6\*300G，6\*600G  单盘容量不要太大，除非纯备份

用途：用于提供生产线上的普通对外提供服务的业务服务器

例如：生产线上的数据库业务、存储业务、图片业务及相关高并发业务

（web http  cache服务），总的来说，如果没有特殊业务需求，SAS磁盘是生产

环境首选的磁盘配置

2、 企业级SATA硬盘：

企业级SATA硬盘，7200-10000转/分，常见的容量为1T和2T，4T，6T，优点是

经济实惠，容量大，从具体的业务需求及性价比考虑，老男孩老师在工作中多用

SATA磁盘做线下不提供服务的数据存储或者并发业务访问不是很大的业务

比如，站点程序及数据库，图片的线下备份等

特性：容量性价比高，一般2T的SATA磁盘交接

3、SSD固态电子盘

特点：容量小，价格贵，速度快。 一般用于数据量小并且有超大规模高并发的业务

（这不是唯一的办法，还可以通过磁盘加内存缓存的技术方式解决这个大规模高并发的问题）

百度，腾讯，360核心业务都会采用SSD磁盘，应用层也必须已经做了各种缓存

特别提示：

大公司如taobao，某些业务可能会根据数据的热度来综合使用分层存储，以达到性价比

最佳的情况。800SSD+500GSATA

1.19 磁盘选购小结：

1、线上的业务，用SAS磁盘

2、线下的业务，用SATA磁盘，磁带库

3、线上高并发、小容量的业务，SSD

4、思想：根据数据的访问热度，智能分析分层存储   SATA +SSD

1.20  淘宝网CDN缓存对象分级存储策略案例

提出问题：

在存储数据中，18KB以下的对象数量占总数量的80%，而其存储量占总量不到40%；同时，80%经常被访问的对象所占用的存储空间不到总量的20%。

分析问题：

以上的问题意味着“热点数据”（即访问频次高的内容）需要更快的性能，而占的空间并不大，而“冷数据”（访问频次低的内容）所需存储量很大，对性能要求不需要高。

解决问题：

因此，服务器引入分层存储机制，单台服务器（实际会多台）的磁盘可由一块80GB的SSD磁盘和两块500GB的SATA盘组成。然后把“热数据”存放在SSD盘上，“冷数据”存放在SATA盘上，冷热数据可以动态调度，从而兼顾性能、容量与成本。另：分层存储调度软件由淘宝开发。

上面的策略是高效，低成本方案，这是我们运维工作需要重视的，实际工作中不可能不考虑成本，而无限制的去提升性能。

一般来说，一块磁盘有一个到数个盘片不等，其中每个盘片的有效盘面对应一个读写磁头，

从上往下从0开始依次编号，不同的磁盘盘面在逻辑上被划分为磁道、柱面以及扇区，

一般在出厂时就设定好了

1.21 相关命令

sync   把内存中的数据刷到磁盘

\[root@oldboy ~\]\# dd if=/dev/sda of=mbr.bin bs=512 count=1

记录了1+0 的读入

记录了1+0 的写出

512字节\(512 B\)已复制，0.000264112 秒，1.9 MB/秒

\[root@oldboy ~\]\# ll mbr.bin

-rw-r--r-- 1 root root 512 4月  24 17:49 mbr.bin

\[root@oldboy ~\]\# free -m

```
         total       used       free     shared    buffers     cached
```

Mem:           988        140        848          0         24         36

-/+ buffers/cache:         79        909

Swap:         1999          0       1999

提示：

1、linux系统的特性是将系统不用的物理内存缓存起来，因此，848不是系统的真实内存

2、系统真正系统内存为909

3、buffer为写入缓冲区，sync将缓存区数据写入磁盘，cache为读出缓存

4、cache为读取数据的缓存区

5、硬盘是机械的，无论是写入还是读取都太慢了，所以读取和写入都是用缓存及缓冲技术

6、门户架构网站都会用缓存技术，来让用户写入读取尽可能不接触磁盘

od   查看二进制文件

partprobe /dev/sdb    通知内核

mkfs.ext4 /dev/sdb1

tune2fs -c -1 /dev/sdb1  不备份

mount /dev/sdb1 /mnt

1.22  磁盘读写原理

磁道数=柱面数

1.22.1   磁盘是按照柱面为单位读写数据

先读取同一个盘面的某一个磁道，读完之后，如果数据没有读完，磁头也不会切换其他

磁道，而是选择切换磁头，读取下一个盘面的同半径的磁道，直到所有盘面的相同半径

的磁道读取完成之后，如果数据还没有读写完，才会切换其他不同半径的磁道，

这个切换磁道的过程称为寻道

1.22.2   不同磁头间的切换是电子切换

而不同磁道间切换需要磁头做径向运动，这个径运动需要步进电机调节，这个动作是机械的切换

磁头寻道是机械运动，切换磁头是电子切换

1.23 磁盘容量

Disk /dev/sda: 10.7 GB, 10737418240 bytes

255 heads, 63 sectors/track, 1305 cylinders

Units = cylinders of 16065 \* 512 = 8225280 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0x00044026

第一种方法：

磁盘容量=512\*扇区数\*磁头数\*磁道数（柱面数）

\[root@oldboy ~\]\# echo "scale=2;\(512\*63\*1305\*255\)/1000000000" \|bc

10.73

第二种方法：

磁盘容量=柱面大小\*柱面数（磁道数）

\[root@oldboy ~\]\# echo "scale=2;\(8225280\*1305\)/1000000000" \|bc

10.73

\[root@oldboy ~\]\# find /var/ \|xargs ls -ld 2&gt;/dev/null\|sort -nk2\|tail -1

-rw-r--r--. 512 root root     6 3月   6 16:31 /var/lib/yum/yumdb/z/b8019061884a679c3b9b867b44c7b9c64182240d-zip-3.0-1.el6-x86\_64/checksum\_type

第2章 分区

2.1  MBR

mbr是磁盘上的一小段扇区, 用来存放代码的空间

grub是一段引导程序

2.2   16B分区表

字节数    说明

1B    State   ：分区状态，0=未激活， 0x80=激活

1B    StartHead ： 分区起始磁头号

2B    StartSC ： 分区起始扇区和柱面号。低字节的低6位为扇区号，高2位为柱面号的第9，10位；高字节为柱面号的低8位

1B    Type  ： 分区类型，如0x0B=FAT32,0x83=linux等，00表示此项未使用

1B    EndHead  ： 分区结束磁头号

2B    EndSC ：分区结束扇区和柱面号，定义同前

4B    Relative ： 线性寻址方式下分区相对扇区地址（对于基本分区即为绝对地址）

4B    Sectors  ： 分区大小（总扇区数）

2.3  分区类型

msdos

gpt

2.4  导出磁盘MBR信息

dd if=/dev/sda of=mbr.bin bs=512 count=1

\[root@c71 ~\]\# od -xa /tmp/mbr.bin

0000000    4658    4253    0000    0010    0000    0000    0100    002c

```
      X   F   S   B nul nul dle nul nul nul nul nul nul soh   , nul
```

0000020    0000    0000    0000    0000    0000    0000    0000    0000

```
    nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul
```

0000040    3fb1    c2f7    777a    0f4b    1eaf    c0ea    ce8e    fb96

```
      1   ?   w   B   z   w   K  si   /  rs   j   @  so   N syn   {
```

0000060    0000    0000    0100    0400    0000    0000    0000    8000

```
    nul nul nul nul nul soh nul eot nul nul nul nul nul nul nul nul
```

0000100    0000    0000    0000    8100    0000    0000    0000    8200

```
    nul nul nul nul nul nul nul soh nul nul nul nul nul nul nul stx
```

0000120    0000    0100    0000    004b    0000    0400    0000    0000

```
    nul nul nul soh nul nul   K nul nul nul nul eot nul nul nul nul
```

0000140    0000    5503    b4b4    0002    0001    1000    0000    0000

```
    nul nul etx   U   4   4 stx nul soh nul nul dle nul nul nul nul
```

0000160    0000    0000    0000    0000    090c    0408    000f    1900

```
    nul nul nul nul nul nul nul nul  ff  ht  bs eot  si nul nul  em
```

0000200    0000    0000    0000    0002    0000    0000    0000    b700

```
    nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul   7
```

0000220    0000    0000    0000    00cc    0000    0000    0000    0000

```
    nul nul nul nul nul nul   L nul nul nul nul nul nul nul nul nul
```

0000240    ffff    ffff    ffff    ffff    ffff    ffff    ffff    ffff

```
    del del del del del del del del del del del del del del del del
```

0000260    0000    0000    0000    0200    0000    0000    0000    0000

```
    nul nul nul nul nul nul nul stx nul nul nul nul nul nul nul nul
```

0000300    0000    0000    0000    0100    0000    8a00    0000    8a00

```
    nul nul nul nul nul nul nul soh nul nul nul  nl nul nul nul  nl
```

0000320    0000    0000    0000    0000    0000    0000    0000    0000

```
    nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul nul
```

\*

0001000

2.5  磁盘分区重点：

1、给磁盘分区的实质就是针对0磁头0磁道1扇区的前446B后面接下来的64B的分区表进行设置

主要是划分起始以及结束磁头号、扇区号及柱面号

2、给磁盘分区的工具有fdisk（适合给小于2T的磁盘分区），parted（擅长给大于2T的磁盘分区，

可以对小于2T的磁盘分区），首选fdisk，只有大于2T 时才去选parted

企业面试题： 一台服务器6块600G的磁盘，raid5后，总大小3T，此时无法装系统，为什么？

解决：

方法1： 做raid5 后，不要重启装系统，在raid界面，继续分一个小的虚拟磁盘vd  200G，用这个

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

2.6  主分区 primary

一般来说，主分区是磁盘上必须存在的分区，一般为磁盘的第一个分区，我们可以在这个分区

上安装操作系统

/boot  主分区

swap  主分区

/      主分区

2.7  扩展分区 extended

扩展分区不能算一个正常的分区，而是一个链接，起到一个指向的作用，我们可以再扩展分区内

建立逻辑分区，扩展分区就像一个虚拟出来的一个小硬盘

一块硬盘只能存在一个扩展分区，并且扩展分区不能直接存放数据

2.8  逻辑分区 logical

逻辑分区必须存在于扩展分区内，在扩展分区可以划分多个逻辑分区，逻辑分区的编号从

5开始

实际应用：主分区和逻辑分区，都可以使用，一般系统安装用主分区，存放数据都可以

2.9   磁盘分区的几个问题范例

1、如果我要将我的一块大磁盘暂时分成四个分区，同时，还希望有其他的空间可以让我

在未来需要的时候再进行分区

3p+1e（1L）剩余空间保留

2p+1e （2L）剩余空间保留

1p+1e（3L） 剩余空间保留

2、假如我有一块SAS硬盘，我想要把磁盘分成6个分区，那么每个磁盘分区在linux系统下

的数字遍号是多少？

1p+1E  /dev/sda1, /dev/sda5……

2p+1E  /dev/sda1,/dev/sda2, /dev/sda5……

3p+1E  /dev/sda1, /dev/sda2, /dev/sda3, /dev/sda5……

生产场景不同角色linux服务器分区案例

[http://oldboy.blog.51cto.com/2561410/634725](http://oldboy.blog.51cto.com/2561410/634725)

[http://oldboy.blog.51cto.com/2561410/629558](http://oldboy.blog.51cto.com/2561410/629558)

2.10  磁盘分区的设备名称

设备名称的定义规则如下，其他的分区可以依次类推：

第一块IDE接口磁盘   /dev/hda

第二块IDE接口磁盘   /dev/hdb

第一块SCSI接口磁盘   /dev/sda

第二块SCSI接口磁盘   /dev/sdb

SATA  SAS 都是 sd开头

每个分区则使用磁盘名称加对应的数字编号表示：

第一块IDE接口磁盘的第1个分区   /dev/hda1

第一块IDE接口磁盘的第5个分区   /dev/hda5

第二块SCSI接口磁盘的第1个分区   /dev/sdb1

第二块SCSI接口磁盘的第5个分区   /dev/sdb5

2.11  fdisk分区

\[root@oldboy ~\]\# fdisk /dev/sdc

WARNING: DOS-compatible mode is deprecated. It's strongly recommended to

```
     switch off the mode \(command 'c'\) and change display units to

     sectors \(command 'u'\).
```

Command \(m for help\): m

Command action

a   toggle a bootable flag

b   edit bsd disklabel

c   toggle the dos compatibility flag

d   delete a partition           删除一个分区

l   list known partition types    查看分区类型对应编号列表

m   print this menu          打印帮助菜单

n   add a new partition        新建一个分区

o   create a new empty DOS partition table

p   print the partition table        打印分区表

q   quit without saving changes   退出程序，不保存

s   create a new empty Sun disklabel

t   change a partition's system id       更改分区类型

u   change display/entry units

v   verify the partition table

w   write table to disk and exit       将操作写入分区表并退出程序

x   extra functionality \(experts only\)

Command \(m for help\): n

Command action

e   extended

p   primary partition \(1-4\)

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

Command \(m for help\): n

Command action

e   extended

p   primary partition \(1-4\)

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

Command \(m for help\): n

Command action

e   extended

p   primary partition \(1-4\)

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

/dev/sdc3              23          33       11264   83  Linux

Command \(m for help\): n

Command action

e   extended

p   primary partition \(1-4\)

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

/dev/sdc3              23          33       11264   83  Linux

/dev/sdc4              34         102       70656    5  Extended

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

/dev/sdc3              23          33       11264   83  Linux

/dev/sdc4              34         102       70656    5  Extended

/dev/sdc5              34          44       11248   83  Linux

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

/dev/sdc3              23          33       11264   83  Linux

/dev/sdc4              34         102       70656    5  Extended

/dev/sdc5              34          44       11248   83  Linux

/dev/sdc6              45         102       59376   83  Linux

Command \(m for help\): w

The partition table has been altered!

Calling ioctl\(\) to re-read partition table.

Syncing disks.

fdisk -cu /dev/sdb

2.12 查看磁盘分区

\[root@oldboy ~\]\# fdisk -l

Disk /dev/sda: 10.7 GB, 10737418240 bytes

255 heads, 63 sectors/track, 1305 cylinders

Units = cylinders of 16065 \* 512 = 8225280 bytes

Sector size \(logical/physical\): 512 bytes / 512 bytes

I/O size \(minimum/optimal\): 512 bytes / 512 bytes

Disk identifier: 0x00044026

Device Boot      Start         End      Blocks   Id  System

/dev/sda1   \*           1          26      204800   83  Linux

Partition 1 does not end on cylinder boundary.

/dev/sda2              26         281     2048000   82  Linux swap / Solaris

Partition 2 does not end on cylinder boundary.

/dev/sda3             281        1306     8231936   83  Linux

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

Device Boot      Start         End      Blocks   Id  System

/dev/sdc1               1          11       11248   83  Linux

/dev/sdc2              12          22       11264   83  Linux

/dev/sdc3              23          33       11264   83  Linux

/dev/sdc4              34         102       70656    5  Extended

/dev/sdc5              34          44       11248   83  Linux

/dev/sdc6              45         102       59376   83  Linux

2.13  查看磁盘分区UUID

\[root@oldboy36 ~\]\# blkid

/dev/sda1: UUID="4c40caf4-8676-4b30-9cd3-9ecdbaa79acd" TYPE="ext4"

/dev/sda2: UUID="5eaa6bea-ffdc-477b-ae6c-94a7fe20838f" TYPE="swap"

/dev/sda3: UUID="70c86ea3-354e-45e3-a2d8-186ecbbc7292" TYPE="ext4"

2.14 格式化

\[root@oldboy ~\]\# partprobe /dev/sdc   强制内核重新查找一次分区表 （分区完成后执行此命令）

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

180 days, whichever comes first.  Use tune2fs -c or -i to override.

\[root@oldboy ~\]\# tune2fs -c -1 /dev/sdc1      取消文件系统自动检查

tune2fs 1.41.12 \(17-May-2010\)

Setting maximal mount count to -1

2.15   partprobe /dev/sdc 报错

Warning: WARNING: the kernel failed to re-read the partition table on /dev/sdb \(Device or resource busy\).  As a result, it may not reflect all of your changes until after reboot

解决方法：

1、重启机器可以解决

2、 lsof /dev/sdb 看一下是否有程式在使用中，如果有可以杀掉进程试试

mkfs.ext4 -b 4096 -I 256 /dev/sdb1

tune2fs -c 0 -i 0 /dev/sdb1

\[root@oldboy ~\]\# dumpe2fs /dev/sdb1 \|egrep -i "\(inode\|block\) size"

dumpe2fs 1.41.12 \(17-May-2010\)

Block size:               4096

Inode size:               256

2.16 xfs分区格式：

yum install xfsprogs kmod-xfs xorg-x11-xfs xfsdump -y

mkfs.xfs -f /dev/sdb1

2.17 挂载

\[root@oldboy ~\]\# mount /dev/sdc1 /mnt/

\[root@oldboy ~\]\# df -h

Filesystem      Size  Used Avail Use% Mounted on

/dev/sda3       7.7G  1.5G  5.8G  20% /

tmpfs           495M     0  495M   0% /dev/shm

/dev/sda1       190M   36M  145M  20% /boot

/dev/sdc1       9.7M  100K  9.0M   2% /mnt

2.18  硬盘被分区后格式化过程

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

要挂载的设备                                       挂载点     挂载类型  挂载选项    备份   磁盘检查

UUID=4bc27c91-8cae-44fb-ba19-4213d1d47326  /mnt  ext4        defaults        0       0

/dev/sdb2               /opt                    ext3    defaults        0 0

要挂载的设备可以是设备路径，也可以是对应的UUID。

特别注意：执行mount -a测试挂载，否则开机可能导致系统起不来。

\[root@c66-mobban1 ~\]\# blkid

/dev/sda1: UUID="88020ecf-caae-4f70-abd5-f01890594ebe" TYPE="ext4"

/dev/sda2: UUID="d3a79fb3-e573-4380-a2f9-2ffa0edaca79" TYPE="swap"

/dev/sda3: UUID="1dd4d340-204d-4ce1-b7b2-e1cefc61f466" TYPE="ext4"

/dev/sdb1: UUID="4bc27c91-8cae-44fb-ba19-4213d1d47326" TYPE="ext4"

/dev/sdb2: UUID="c8e8b094-166b-40ae-9155-ac29da06c80e" SEC\_TYPE="ext2" TYPE="ext3"

\[root@c66-mobban1 ~\]\# tail -2 /etc/fstab

UUID=4bc27c91-8cae-44fb-ba19-4213d1d47326  /mnt  ext4   defaults        0 0

/dev/sdb2               /opt                    ext3    defaults        0 0

2.19  对损坏的磁盘做手动检查

方法1：

fsck  -C  -f  -t  ext4  /dev/sdb1

方法2：

\[root@oldboy ~\]\# badblocks -sv /dev/sdb1

Checking blocks 0 to 20479

Checking for bad blocks \(read-only test\): done

Pass completed, 0 bad blocks found.

2.20  如何检查并修复/dev/hda5

fsck -C -t msdos -a /dev/hda5

e2fsck -p /dev/hda5

作业：fstab被破坏了，导致系统无法启动，如何修复？

使用光盘引导进入救援模式，或者在单用户模式下，使用mount / -o remount 重新挂载提权，然后修改/etc/fstab文件，修改正确后重启即可

2.21 parted  分区

不写单位默认为MB

实验：100M盘

parted /dev/sdb mklabel gpt Yes

parted /dev/sdb mkpart primary 0 10 Ignore

parted /dev/sdb mkpart primary linux-swap 11 21 Ignore

parted /dev/sdb mkpart logical ext4 22 32 Ignore

parted /dev/sdb p

parted /dev/sdb rm 3

fdisk   非交互式分区：

parted  /dev/sdb  mklabel  bsd yes     将硬盘分区表由gpt格式转换为bsd格式（MBR）

vi  fdisk.txt

n         新建一个分区

p           primary分区

1           分区编号

```
        起始扇区（可以不写）
```

+100M        结束扇区 （可以直接写大小）

p            打印分区表

w            保存修改并退出

fdisk  /dev/sdb &lt; fdisk.txt        执行分区

ll  /dev/sdb\*                    检查分区是否成功

mkfs.ext4   /dev/sdb1            格式化分区

mount  /dev/sdb1  /mnt            挂载分区

df -h \|grep /dev/sdb1

echo  -e  "n\np\n1\n\n+10M\nn\np\n2\n\n+10M\nw" \|fdisk  /dev/sdb

partprobe

注意：  parted  的操作都是实时的，千万不能在生产环境中测试

实验：100M盘

parted /dev/sdb mklabel gpt Yes

parted /dev/sdb mkpart primary 0 10 Ignore

parted /dev/sdb mkpart primary linux-swap 11 21 Ignore

parted /dev/sdb mkpart logical ext4 22 32 Ignore

parted /dev/sdb p

2.22  fdisk  parted  ext4  xfs

传统的fdisk分区不支持2T以上的磁盘分区，而parted分区可以支持，而ext4格式不支持16T以上的磁盘空间分区，必须使用xfs分区

2TB以上磁盘分区、制作文件系统：

分为两个主分区\(先创建磁盘标签mklable ，再创建分区mkpart分区类型\)

\[root@localhost ~\]\# parted /dev/sdb         \# 使用parted来对GPT磁盘操作，进入交互式模式

\(parted\) mklabel gpt                  \# 将MBR磁盘格式化为GPT

\(parted\) print                                 \#打印当前分区

\(parted\) mkpart primary 0 4.5TB                   \# 分一个4.5T的主分区

\(parted\) mkpart primary 4.5TB 12TB                          \# 分一个7.5T的主分区

\(parted\) print                                               \#打印当前分区

\(parted\) quit                                                退出

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

