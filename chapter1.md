# 第一节 上节知识点回顾

服务器硬件

CPU

主板

内存

硬盘

高并发  内存---&gt; 磁盘

中小企业 数据写入磁盘

运维职责：

1、数据

2、7\*24不宕机

3、提升用户体验

第2章 Linux简介

2.1 什么是操作系统

操作系统是一个用来协调、管理和控制计算机硬件和软件资源的系统程序，它位于硬件和应用程序之间。\\(内核和调用接口\\)

Linux系统分为：内核+shell+扩展软件

操作系统，英文名称Operating System，简称OS，是计算机系统中必不可少的基础系统软件，它是应用软件运行及用户操作的必备的基础环境支撑，是计算机系统的核心。

操作系统的作用是管理和控制计算机系统中的硬件和软件资源，例如：它负责直接管理计算机系统各种硬件资源，如对CPU、内存、磁盘等的管理，同时对系统资源供需的优先次序进行管理。操作系统还可以控制设备输入、输出以及操作网络与管理文件系统等事务。同时，它负责对计算机系统中各类软件资源的管理。例如各类应用软件的安装、运行环境设置等。图1-1给出了操作系统与计算机硬件、软件之间的关系示意图。

![](/assets/import.png)

                                            图1-1     操作系统与计算机软硬件关系示意图

目前PC\(Intel x86系列\)计算机上比较常见的操作系统有Windows、Linux、DOS、Unix等。

思考：世界上什么操作系统使用率最高?



2.1.1 什么是Linux？

```
类似Windows，Linux也是一个操作系统软件，Linux是一套开放源代码程序的、并可以自由传播的类Unix操作系统软件，支持多用户、多任务并且支持多线程和多CPU的操作系统。

Linux系统主要被应用于服务器端，嵌入式开发和个人PC桌面3打领域，其中服务器端领域是重中之重。

BAT\(百度、阿里、腾讯\)

我们熟知的大型、超大型互联网企业\(百度、Sina、淘宝等\)都在使用Linux操作系统为其服务器端程序运行的平台，全球及国内排名前十的网站使用的主流操作系统都是Linux系统。

从杀手给你们的内容可以看出，Linux操作系统之所以如此流行，是因为它具有如下一些特点：
```

    是开放源代码的程序软件，可自由修改。

    Unix系统兼容，具备几乎所有Unix的优秀特性。

    可自由传播，无任何商业化版权制约。

    适合Intel等x86 CPU系列架构的计算机。

技巧：学会对阶段性知识的总结是学好运维的关键

```
滚雪球的方式来学习Linux，不断积累。
```

2.2 Linux起源

2.2.1 Unix的历史

```
Unix系统于1969年在AT&T的贝尔实验室诞生，20世纪70年代，它逐步盛行，这期间，又产生了一个比较重要的分支，就是大约1977年诞生的BSD\(Berkeley Software Distribution\)系统。从BSD系统开始，各大厂商及商业公司开始根据自身的硬件架构，并以BSD系统为基础进行Unix系统研发，从而产生了各种版本的Unix系统，例如：SUN公司的Solaris，IBM公司的AIX，HP公司的HP UNIX等。图1-3给出了Unix系统诞生、发展的时间及版本分支介绍，供读者参考。
```

2.4 Unix的5打特性

    技术成熟，可靠性高

    极强的可伸缩性

Unix支持CPU处理器体系架构非常多，包括Intel/AMD及HP-PA、MIPS、PowerPC、UItraSPARC、ALPHA等RISC芯片，以及SMP、MPP等技术。

提示：可能由于早期各大厂商都基于Unix进行适合自己的硬件开发，因此，Unix支持的CPU架构才更多。

    强大的网络功能

Internet互联最重要的协议TCP/IP就是Unix上开发和发展起来的。此外，Unix还支持非常多的常用的网络通信协议，如NFS、DCE、IPX/SPX、SLIP、PPP等。

    强大的数据库支持能力

Oracle、DB2、Sybase、Informix等大型数据库，都把Unix作为其主要的数据库开发和运行平台，一直到目前为止，依然如此。

    强大的开发功能

正是Unix促使了C语言的诞生

2.5 Unix操作系统的革命

```
70年代中后期，由于各厂商及商业公司开发的Unix及内置软件都是针对自己公司特定硬件的，因此在其他公司的硬件上基本上无法直接于运行。

70年代末，Unix有面临了突如其来的被AT&T回收版本的重大问题，特别是要求禁止对学生群体提供Unix系统元代码。

也是在80年代初期，同样是由于之前的Unix系统版本和源代码限制等问题，使得当时大学里教学Unix系统的束缚很大。因此，当时一个大学的教授，名字为Andrew Tanenbaum（谭宁邦），自己开发出一个类Unix系统，并且可以运行于x86 PC平台，这个系统的名称为：Minix。

老男孩补充：由于谭宁邦教授开发的这个Minix系统的目的只是用于教学，因此，Minix系统的功能无法满足商用的需求，但是Minix的产生对于Linux的诞生有事至关重要的一个部分。

1984年，Richard Stallman\(理查德•斯托曼\)发起了开发自由软件的运动，并成立了自由软件基金会\(Free Software foundation，FSF\)和GNU项目。

当时发起来这个自由软件运动和创建GNU项目的其实很简单，就是想开发一个类似Unix系统、并且是自由软件的完整操作系统，也就是要解决70年代末Unix版权问题以及软件源代码面临关闭的问题，这个系统叫作GNU操作系统。
```

老男孩补充：这个GNU系统后来没有流行起来。现在的GNU系统通常是使用Linux系统内核，以及使用了GNU项目贡献的一些组件加上其他相关程序组成，这样的组合被成为GNU/Linux操作系统。

2.6 Linux诞生

```
Linux系统的诞生开始与芬兰赫尔辛基大学的以为计算机系的学生，名字为Linus Torvalds。

Linux的标志和吉祥物为一只名字叫作Tux的企鹅——Torvalds' Unix，如图1-2所示。
```

图1-2

2.7 Linux的发展过程

```
1.Linux的发展历程介绍
```

1. 1984年，Andrew S. Tanenbaum开发了用于教学的Unix系统，名为Minix。

2. 1989年，Andrew S. Tanenbaum将Minx系统运行于x86的PC计算机平台。

3. 1990年，芬兰赫尔辛基大学学生Linus Torvalds首次接触Minix系统。

4. 1991年，Linus Torvalds开始在Minix上编写各种驱动程序等操作系统内核组件。

5. 1991年底，Linus Torvalds公开了Linux内核源码0.02版\([http://www.kernel.org\)，注意这里公开的Linux内核源码并不是我们现在使用的Linux系统的全部，而仅仅是Linux内核kernel部分的代码。](http://www.kernel.org%29，注意这里公开的Linux内核源码并不是我们现在使用的Linux系统的全部，而仅仅是Linux内核kernel部分的代码。)

6. 1993年，Linux 1.0版发型，Linux转向GPL版权协议。

7. 1994年，Linux的第一个商业发行版Slackware问世。

8. 1996年，美国国家标准技术局的计算机系统实验室确认Linux版本1.2.13\(由Open Linux公司打包\)符合POSIX标准。

9. 1999年，Linux的简体中文版问世。

10. 2000年后，Linux系统日趋成熟，涌现大量基于Linux服务器平台的应用，并广泛用于基本ARM技术的嵌入式系统中。

2.Linux发展历程中相关人物

```
我们一定要向前辈们致以深深的敬意，没有他们，就没有今天优秀的Linux系统存在了\(图1-3\)
```

图1-3     Linux发展历程中相关人物

第3章 Linux核心概念

3.1 自由软件与Free Software Foundation

```
简单地理解，自由软件的核心就是没有商业化软件版权制约，源代码开放，可无约束自由传播。
```

注意：自由软件强调的是权利问题，而非是否免费的问题。大家一定要理解这个概念，自由软件中的自由是“言论自由”中的“自由”，而不是“免费啤酒”中的“免费”。

```
自由意味着freedom，二免费意味着free，这是完全不同的概念，例如：Red Hat Linux自由但不免费，CentOS Linux是自由且免费的。

自由软件关乎使用者运行、复制、发布、研究、修改和改进该软件的自由。 
```

3.2 Free Software基金会FSF

```
FSF\(Free Software Foundation\)的中文意思是自由软件基金会，是Richard Stallman于1984年发起和创办的。FSF的主要项目是GNU项目。GNU项目本身产生的主要软件包括：Emacs编辑软件、gcc编译软件、bash命令解释程序和编程语言，以及gawk\(GNU sawk\)等。
```

3.3 GNU知识

```
GNU的全称为：GNU's not unix，意思是“GNU不是Unix”，GNU计划，又称革奴计划，是由Richard Stallman在1983年9月27日公开发起的，旨在开发一个类似 Unix ，且为 自由软件 的完整的操作系统： GNU 系统。在1985年Richard Stallman又创立了自由软件基金会（Free Software Foundation）来为GNU计划提供技术、法律以及财政支持。前面已经提到，GNU项目主要目标是建立一套完全自由和可移植的类Unix操作系统。

但是由于GNU 的内核尚未完成，所以 GNU 使用 Linux 作为其内核。GNU 和 Linux 以这样的方式组合成为 GNU/Linux 操作系统。

到1991年，Linux内核发布的时候，GNU项目已经完成了除系统内核之外各种必备软件的开发。在Linux Torvalds和其他开发人员的努力下，GNU项目的部分组件又运行到了Linux内核之上，例如：GNU项目里的Emacs、gcc、bash、gawk、nano等，至今都是Linux系统中的重要组件。
```

图标：

3.4 GPL知识

```
概念：

GPL\(General Public Licese\)叫作：GNU通用公共许可证。

是GNU项目的三个协议条款之一，是一个最著名的开源许可协议，开源社区最著名的Linux内核就是在GPL许可下发布的。它并非由自由软件基金会所发表，亦非使用GNU通用公共授权的软件的法定发布条款─直有GNU通用公共授权英文原文的版本始具有此等效力。

那么到底什么事GPL协议了？这里我们简要说明一下：

简单的理解，GPL许可的核心，是保证任何人有共享和修改自由软件的自由，任何人有取得、修改和重新发布自由软件源代码的权利，但是必须同时给出具体更改的源代码。

虽然整个Linux内核是基于GNU通用公共许可的，但是Linux内核并不是GNU计划的一部分。

FSF\(基金会\)                GNU\(项目\)                emacs,gcc,bash,gawk

GNU\(项目\)                GPL\(员工守则\)            自由传播，修改源代码，但是必须把修改的代码发布出来。
```

3.5 Linux系统组成

```
Linux操作系统 = Linux内核 + GNU项目软件 + 必要的应用程序

                表1-1Linux系统各组成部分的贡献人员
```

Linux内核    GNU组件\(gcc,bash等\)    其他必要应用程序

开发者Linus Torvalds    项目发起人Richard Stallman    BSD Unix和X Windows以及成千上万的程序员

图1-4         为Linux系统的核心组成原理示意图。

第4章 Linux特点

4.1 Linux为什么受欢迎

```
Linux系统之所以受到广大计算机爱好者的喜爱，主要原因有两个：
```

    一是，Linux属于开源软件，用户不用支付任何费用就可以获得系统和系统的源代码，并且可以根据自己的需要对源码进行必要的修改，无偿使用，无约束地自由传播。

    Linux具有Unix的全部优秀特性，任何可以获得Unix几乎所有优秀功能，并且Linux系统更开放，社区开发和全世界的使用者也更活跃。

第5章如何选择Linux发行版

5.1 Linux的发行版介绍

```
Linux内核\(kernel\)版本主要有4个系列，分别为Linux kernel2.2、Linux kernel2.4、Linux kernel 2.6、Linux kernel3.x，更多更新的内核版本请浏览https://www.kernel.org。

Linux的发行商包括Slackware、Redhat、Debian、Fedora、TurboLinux、Mandrake、SUSE、CentOS、Ubuntu、红旗，麒麟••••••

下面来看看期中几个重要的发型版本:
```

    Redhat： Redhat Linux9.0的内核为2.4.20。在版本9.0后，Redhat不在遵循GPL协议，成为收费产品\(但仍开源\)，发展的新版本一次为Redhat3.x、Redhat4.x、Redhat5.x、Redhat6.x、Redhat7.x、Redhat Enterprise6.x。

    Fedora: 为Redhat的一个分支，仍遵循GPL协议，可以认为是Redhat预发布版。\(就像是游戏的公测版\)

    CentOS\(community Enterprise Operating System\)：与Redhat做到二进制级别的一模一样，Redhat的另一个重要分支，以Redhat所发布的源代码重建符合GPL许可协议的Linux系统，即将Redhat Linux源代码的商标Logo以及非自由软件部分去除在编译而成的版本，目前CentOS已被Redhat公司收购，但仍开源免费，CentOS Linux是国内互联网公司使用最多的Linux系统版本，也是本书的"主人公"，本书后面所有的内容讲解都是基于CentOS这个操作系统的，绝大部分内容几乎无需任何修改同样适合其他操作系统版本。

提示：有关Linux操作系统，记住Redhat、CentOS、Ubuntu、Fedora、SUSE、Debian等即可。

5.2 选择适合的Linux系统学习

5.2.1 Linux发行版本应用场景

Linux发行版本选择

Linux桌面系统    Ubuntu\(开发人员开发平台\)

服务器端Linux系统    首选Redhat\(有钱任性\)或者CentOS

如果对安全要求很高    Debian或FreeBSD

使用数据库高级服务或电子邮件网路哦用户    SUSE

想新技术，新功能是RHEL和CentOS的测试版或预发布版    Fedora

Fedora=稳定之后=&gt;Redhat=去Logo去除收费=&gt;CentOS

中文    红旗Linux，中标麒麟Linux

5.2.2 选择CentOS  Linux版本

```
本诉讲解的Linux运维技术主要是基于CentOS x86\_64 Linux的，绝大部分知识几乎无需任何修改同样适用于Redhat Linux等同源或类似Linux系统版本。

下面是CentOS的主流版本在国内互联网企业的使用现状说明：
```

    CentOS 5系列：占25%左右，主流版本有CentOS 5.5 、CentOS 5.8、CentOS 5.10、CentOS 5.11，不推介新手学习了。=&gt;Linux kernrl 2.4

    CentOS 6系列：占45%左右，主流版本有CentOS 6.2、CentOS 6.4、CentOS 6.6、CentOS 6.8，推介新手学习。=&gt;Linux kernrl 2.6

    CentOS 7系列：最新的系统，目前正式使用的企业不多，因此不建议去玩它，最好学习目前企业使用较多的6系列，等过2年企业都上了CentOS7的系统，就可以轻松转过去了，不要盲目选择较高的版本。

小面试题：你们公司服务器使用的版本系统是什么？

CentOS 6.8 X86\_64 内核版本3.6.32

面试技巧：大家被面试官问及使用什么样操作系统时，一定要一次性说出来\(系统版本、内核版本、32位和64位\)，例如：我们工作中使用的是CentOS 6.7 x86\_64位Linux系统，内核版本为2.6.32-573，这才是一个合格的Linux运维人员的表现。

第6章 总结

1. 了解什么是操作系统以及操作系统简单原理图

2. 了解Unix的发展史

3. 了解市面上常见的Unix系统版本

4. 了解Unix及Linux诞生的几个关键人物

5. 重点了解GNU，GPL知识

6. 了解Linux系统的特性

7. 了解Linux系统常见的发行版本，不同场景选择

8. 重点了解CentOS和Redhat的区别和联系

9. 了解CentOS各个版本的应用场景及企业应用情况

10. 学会搭建学习Linux的环境

注意：最好口述表达出上述了解的内容

# 



