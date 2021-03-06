#### 1、RAID介绍及各RAID的分类

把多个物理磁盘通过不同的技术方式组成磁盘阵列，这个不同的技术方式为RAID级别

生产环境常用的raid级别：RAID 0 , RAID 1 ,RAID 5 , RAID 10

![](/assets/tab35-1.png)

硬RAID

在实际的生产场景工作中，基于硬件的RAID解决方案应该是我们的首选

互联网公司常用的生产DELL服务器、默认支持RAID 0,1

如果 RAID 5 ，10  需要买RAID卡

RAID 最直接的好处：

1、 提升数据安全性

2、提升数据读写性能

3、提供更大的单一逻辑磁盘数据容量存储

##### RAID 0  一块盘到多块盘，容量是所有盘之和

##### RAID 1  必须2块盘，容量损失一块盘

##### RAID 5  最少三块盘，只损失一块盘容量

##### RAID 10  最少4块盘，必须偶数磁盘，损失一半的容量

#### 2、RAID0介绍及应用场景

条带化（或 条带模式）具有最高的存储性能

原理：把连续的数据分散到多个磁盘上存取

生产应用场景：

1、负载均衡集群下面的多个相同RS节点服务器

2、分布式文件存储下面的主节点或chunk server

3、mysql主从复制的多个slave服务器

4、对性能要求很高，对冗余要求很低的相关业务

![](/assets/tab35-2.png)

#### 3、RAID1介绍及应用场景

镜像：把写入一个磁盘的数据全部自动复制到另外一个磁盘上，实现存储双份数据

只能两块盘，整个raid大小为最小的那块磁盘容量

![](/assets/tab35-3.png)![](/assets/tab35-4.png)

#### 4、RAID5介绍及应用场景

至少需要三块磁盘，可以提供热备盘实现故障恢复只允许坏一块盘，系统会根据存储的奇偶校验

重建数据

容量： 损失一块盘的容量

![](/assets/tab35-5.png)

![](/assets/tab35-6.png)

![](/assets/tab35-7.png)![](/assets/tab35-8.png)

#### 5、RAID10

与RAID 1 一样的数据安全保障，与RAID 0近似的存储性能

最少4块盘，必须偶数硬盘，不管硬盘多少，都损失一半的容量

![](/assets/tab35-9.png)![](/assets/tab35-10.png)

#### 6、各Raid级别总结

#### ![](/assets/tab35-11.png)

#### 练习题：

简述各RAID级别的优缺点和应用场景

