## 1.1 服务器、服务器分类、运维职责

### 一、服务器

服务器，也称伺服器，是提供计算服务的设备。由于服务器需要响应服务请求，并进行处理，因此一般来说服务器应具备承担服务并且保障服务的能力。

服务器的构成包括[处理器](https://baike.baidu.com/item/处理器)、[硬盘](https://baike.baidu.com/item/硬盘)、[内存](https://baike.baidu.com/item/内存)、[系统](https://baike.baidu.com/item/系统)[总线](https://baike.baidu.com/item/总线)等，和通用的计算机架构类似，但是由于需要[提供](https://baike.baidu.com/item/提供)高可靠的服务，因此在处理能力、稳定性、可靠性、安全性、可扩展性、可管理性等方面要求较高。

在网络环境下，根据服务器提供的服务类型不同，分为文件服务器，[数据库服务器](https://baike.baidu.com/item/数据库服务器)，应用程序服务器，WEB服务器等。

### 二、服务器的分类

#### 从外形分类

#### 1、机架式服务器

机架式服务器的外形看来不像计算机，而像“抽屉”，有1U（1U=1.75英寸=44.45毫米）、2U、4U等规格。机架式服务器安装在标准的19英寸机柜里面。这种结构的多为功能型服务器

![](/assets/图2-18.png)

![](/assets/图2-19.png)

#### 2、刀片服务器

箱子里摆放整齐的书

所谓刀片服务器（准确的说应叫做刀片式服务器）是指在标准高度的机架式机箱内可插装多个卡式的服务器单元，实现高可用和高密度。每块“刀片”实际上就是一块系统主板。它们可以通过“板载”硬盘启动自己的操作系统，如Windows NT/2000、Linux等，类似于一个个独立的服务器，在这种模式下，每一块母板运行自己的系统，服务于指定的不同用户群，相互之间没有关联，因此相比较于机器式服务器和机柜式服务器，单片母板的性能较低，不过，管理员可以使用系统软件将这些母板集合成一个服务器集群。在集群模式下，所有的母板可以连接起来提供高速的网络环境，并同时共享资源，为相同的用户群服务。在集群中插入新的“刀片”，就可以提高整体性能。而由于每块“刀片”都是热插拔的，所以，系统可以轻松地进行替换，并且将维护时间减少到最小。

![](/assets/图2-20.png)

![](/assets/图2-21.png)

#### 3、塔式服务器-更强壮的计算机

塔式服务器（Tower Server）应该是最容易理解的一种服务器结构类型，因为它的外形以及结构都跟立式PC差不多，当然，由于服务器的主板扩展性较强、插槽也多出一堆，所以个头比普通主板大一些，因此塔式服务器的主机机箱也比标准的ATX机箱要大，一般都会预留足够的内部空间以便日后进行磁盘和电源的冗余扩展。但这种类型服务器也有不少局限性，在需要采用多台服务器同时工作以满足较高的服务器应用需求时，由于其个体比较大，占用空间，也不方便管理，便显然也很不适合。

![](/assets/图2-22.png)

![](/assets/图2-23.png)

#### 

#### 三、运维职责

1. 网站数据不能丢失      \#---&gt; 大片不能丢
2. 网站7\*24小时运行      \#---&gt; 大片随时看
3. 提升用户体验          \#---&gt; 打开大片的速度快

要求服务器稳定性比普通家用机高

#### 企业案例：提升用户体验的网站解决方案

看需求，选方案

门户\(大网站\)极端案例：大并发写入案例\(抢红包、发微博\)

高并发、大数据量“写”数据：会把数据先写到内存，积累一定的量后，然后再定时或者定量的写到磁盘\(减少磁盘IO Input/Output 磁盘读写\)，最终还是会把数据加载到内存中再对外提供访问。

#### 1、高并发写入\(同一时间段内，同时发生的访问\) {#一、高并发写入同一时间段内，同时发生的访问}

![](/assets/图2-12.png)

特点：

a. 优点：写数据到内存，性能高速度快\(微博，微信，秒杀\)

b. 缺点：可能会丢失一部分在内存中还没有来得及存入磁盘的数据

解决数据不丢的方法：

a. 服务器主板上安装蓄电池，在断电的瞬间把内存数据回写到磁盘。

b. UPS\(一组蓄电池\)不间断供电\(持续供电10分钟，IDC数据中心机房UPS1小时\)。

UPS（Uniterruptible Power System/Unintertuptible Power Supply）,即不间断电源，是将蓄电池\(多为铅酸免维护蓄电池\)与主机 相连接，通过主机逆变器等模块电路将直流电转换成市电的系统设备

c. 选双路电的机房，使用双电源、分别接不同路的电，服务器要放到不同的机柜、地区

#### 2、中小企业读取写入过程 {#二、中小企业读取写入过程}

![](/assets/图2-13.png)

#### 

#### 练习题：

1、简述什么是服务器？

2、服务器的分类

3、企业案例：提升用户体验的解决方案？

