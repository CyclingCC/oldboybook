### 一、Linux发展历史及重要人物

#### 1、Linux发展历史

1. 1984年，Andrew S. Tanenbaum开发了用于教学的Unix系统，名为Minix。

2. 1989年，Andrew S. Tanenbaum将Minx系统运行于x86的PC计算机平台。

3. 1990年，芬兰赫尔辛基大学学生Linus Torvalds首次接触Minix系统。

4. 1991年，Linus Torvalds开始在Minix上编写各种驱动程序等操作系统内核组件。

5. 1991年底，Linus Torvalds公开了Linux内核源码0.02版\([http://www.kernel.org\)，注意这里公开的](http://www.kernel.org%29，注意这里公开的)       linux内核源码并不是我们现在使用的Linux系统的全部，而仅仅是Linux内核kernel部分的代码。

6. 1993年，Linux 1.0版发型，Linux转向GPL版权协议。

7. 1994年，Linux的第一个商业发行版Slackware问世。

8. 1996年，美国国家标准技术局的计算机系统实验室确认Linux版本1.2.13\(由Open Linux公司打包\)         符合POSIX标准。

9. 1999年，Linux的简体中文版问世。

10. 2000年后，Linux系统日趋成熟，涌现大量基于Linux服务器平台的应用，并广泛用于基本ARM技术

#### 2、linux发展中重要人物

![](/assets/图1-3.png)

图1.1.5-linux系统诞生发展过程中关键代表人物

第一个里程碑：Unix诞生-贝尔实验室

第二个里程碑：谭教授-谭宁邦

开发Minix，用于教学

第三个里程碑：斯托曼-目标:创建一个操作系统-替代你Unix ，自由软件

创建公司:FSF 自由软件基金会

项目：GNU=GNU is not Unix

守则：GPL通用公共许可

第四个里程碑：托瓦斯-91开发出来linux内核

GNU\(软件\)/Linux\(内核\)

当今使用的linux是由linux GNU软件 shell 托瓦斯内核 组成

### 二、Linux常见发行版对比

Linux内核\(kernel\)版本主要有4个系列，分别为Linux kernel2.2、Linux kernel2.4、Linux kernel 2.6、Linux kernel3.x，更多更新的内核版本请浏览[https://www.kernel.org。](https://www.kernel.org。)

```
Linux的发行商包括Slackware、Redhat、Debian、Fedora、TurboLinux、Mandrake、SUSE、CentOS、Ubuntu、红旗，麒麟••••••
```

下面来看看期中几个重要的发型版本:

1、Redhat： Redhat Linux9.0的内核为2.4.20。在版本9.0后，Redhat不在遵循GPL协议，成为收费产品\(但仍开源\)，发展的新版本一次为Redhat3.x、Redhat4.x、Redhat5.x、Redhat6.x、Redhat7.x、Redhat Enterprise6.x。

2、Fedora: 为Redhat的一个分支，仍遵循GPL协议，可以认为是Redhat预发布版。\(就像是游戏的公测版\)

3、    CentOS\(community Enterprise Operating System\)：与Redhat做到二进制级别的一模一样，Redhat的另一个重要分支，以Redhat所发布的源代码重建符合GPL许可协议的Linux系统，即将Redhat Linux源代码的商标Logo以及非自由软件部分去除在编译而成的版本，目前CentOS已被Redhat公司收购，但仍开源免费，CentOS Linux是国内互联网公司使用最多的Linux系统版本，也是本书的"主人公"，本书后面所有的内容讲解都是基于CentOS这个操作系统的，绝大部分内容几乎无需任何修改同样适合其他操作系统版本。

![](/assets/图1-6.png)

提示：有关Linux操作系统，记住Redhat、CentOS、Ubuntu、Fedora、SUSE、Debian等即可。Redhat与      CentOS的区别和联系，有时会被面试官问到，需要重点了解

### 三、linux发行版本应用场景

Linux发行版本选择

| **Linux桌面系统** | Ubuntu（乌班图）\(开发人员开发平台\) |
| :--- | :--- |
| **服务器端Linux系统** | 首选Redhat（免费下载和使用更新升级）\(有钱任性\)或者CentOS这两者当中选CentOS（与redhat一模一样） |
| **如果对安全要求很高** | Debian或FreeBSD |
| **使用数据库高级服务或电子邮件网路哦用户** | SUSE FreeSUSE（德国多） |
| **想新技术，新功能是RHEL和CentOS的测试版或预发布版** | FedoraFedora=稳定之后=&gt;Redhat=去Logo去除收费=&gt;CentOS |
| **中文** | 红旗（Red Flag）Linux，中标麒麟（Kylin）Linux |



