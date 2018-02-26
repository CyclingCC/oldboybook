### 一、计算机服务器的主要构成

![](/assets/图2-3.png)

#### 1、机箱

##### 服务器的机箱

![](/assets/图2-4.png)

##### **家用电脑的机箱**

![](/assets/图2-5.png)

#### 2、电源

功能：保障电脑的电源供应

作用：一个合格的电源对电脑的作用是至关重要的，电源就犹如人体的心脏，随时提供新鲜的血液，即使用再聪明的头脑或再敏捷的身手也离不开电脑电源。劣质的电源不仅直接影响电脑的正常的使用，对主板、显卡等其它配件造成损害，而且这种电源所产生的电磁辐射，对人身健康也构成了潜在的威胁。在服务器领域，电源的作用更加重要，因此，服务器一般提供双电源\(双冗余电源\)

1. 数据和7\*24
2. 两个电源

![](/assets/图2-6.png)

#### 3、主板 {#123-主板}

主板和CPU都是电脑中最关键的部件

所有的板卡必须通过主板发挥作用，主板性能和质量的好坏直接影响到整个系统。

电脑主板按不同的架构标准和各种不同的主要部件、接口组合而成

![](/assets/图2-7.png)

#### 4、CPU\(中央处理器\) {#124-cpu中央处理器}

功能：也就是负责运算和控制的控制中心，是电脑的最关键部位，是计算机的头脑

作用：相当于人的大脑一样，在计算机中进行的任何操作\(数据的输入，存储，程序的运行，屏幕的显示，结果的打印\)都在CPU的控制下完成的。CPU比计算机中任何部件都更能决定计算机的工作速度和效率

双CPU时，只能同时装同一型号的

![](/assets/图2-8.png)

![](/assets/图2-9.png)

#### 5、CPU风扇 {#125-cpu风扇}

功能：为CPU降温

作用：如果一开机CPU的温度就很高，时间长了搞不好就是一屡黑烟，然后上千大元的CPU就完了，所以，选一个好的风扇是十分重要的

![](/assets/图2-10.png)

#### 6、BIOS芯片 {#126-bios芯片}

BIOS\(basic input output system\) 芯片\(CMOS芯片\)：负责主板通电后各部件自检，设置，保存，一切正常后才能启动操作系统。记录了电脑最基本的信息，是软件与硬件打交道的最基础的桥梁，没有它电脑就不能工作。

常见的三种BIOS：Award、AMI、Phoenix

![](/assets/图2-11.png)

#### 7、内存

CPU和磁盘之间的缓冲设备，是临时存储器\(存放数据的\)，断电数据丢失。

一般程序运行的时候会被调度到内存中执行，服务器关闭或程序关闭之后，数据自动从内存中释放掉。

片===硬盘===程序

播放器===被运行起来的程序===进程

没完没了的播放片===（住院）===一直运行的程序===守护进程

1. 程序：c/php/java，代码文件，静态的，放在磁盘里的数据。
2. 进程：正在运行着的程序，进程运行就是系统把程序放在内存里执行。
3. 守护进程\(daemon 低萌\)：持续保持运行的程序

#### 8、内存和程序的区别

电影放在磁盘里就是程序

1. 看片放到内存里就相当于进程
2. 计算机重启，内存的数据会释放掉

#### 9、CPU处理器

相当于人体的大脑，负责计算机的运算和控制，是服务器性能效率的最核心部件。

常见品牌：Inter，AMD

![](/assets/图2-14.png)

一般的企业里的服务器，CPU颗数2-4颗，单颗CPU是四核。内存总量一般是16-256G（32G，64G）

1. 做虚拟化的宿主机\(eg：安装vmware的主机\)，CPU颗数4-8颗，内存总量一般是48-128G，6-10个虚拟机

代表图片：

![](/assets/图2-15.png)

#### 10、磁盘

磁盘就是永久存放数据的存储器，磁盘上也是有缓存的\(芯片\)。

常用的磁盘\(硬盘\)都是3.5英寸的\(ide,sas,sata\)，常规的机械硬盘，读取（性能不高）性能比内存差很多，所以，在企业工作中，我们才会把大量的数据缓存到内存，写入到缓冲区，这是当今互联网网站必备的解决网站访问速度慢的方案。

磁盘接口或类型：IDE，SCSI，SAS，SATA，SSD（电子的），IDE，SCSI退出历史舞台。

性能与价格：SSD（固态）&gt;SAS&gt;SATA

磁盘大小

* 1024
* 1byte=8bit 1K=1024byte 1M=1024K
* 1G=1024M 1T=1024G 1PB=1024T
* 字节\(byte\)：8个二进制位为一个字节\(B\)

市面上卖硬盘的都是按1000计算，号称500G硬盘=500\*1000B\*1000KB\*1000MB

#### 常见的硬盘接口及类型

![](/assets/图2-16.png)

#### 磁盘接口优化

1、常规正式工作场景（线上的生产环境）主选SAS（结合SATA和SCSI的优点）硬盘（转速是15000转/分，机械磁盘转数高的性能好）

2、比较核心的业务SAS

生产环境==&gt; 已经对外提供服务的环境

3、不对外提供访问的服务器，例如：线下的数据备份，可选SATA（7200-10000转/分）

SATA特点：容量大，价格便宜，但是速度比较慢

4、高并发访问，小数据量，可以选择SSD

5、企业级硬盘适合7\*24使用的，一般较贵

6、企业网站来讲，都会尽量让用户从内存中读取数据，而不是硬盘

7、几乎企业运维和架构师的网站哟花、服务器、软件的优化核心，都是磁盘和内存的使用比例优化

![](/assets/图2-17.png)

### 小结 {#43-小结}

缓存无处不在，电脑硬件、网站集群
