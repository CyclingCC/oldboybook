#### Linux的发行版介绍

![](/assets/图1-6.png)

inux内核\\(kernel\\)版本主要有4个系列，分别为Linux kernel2.2、Linux kernel2.4、Linux kernel 2.6、Linux kernel3.x，更多更新的内核版本请浏览[https://www.kernel.org。](https://www.kernel.org./)

Linux的发行商包括Slackware、Redhat、Debian、Fedora、TurboLinux、Mandrake、SUSE、CentOS、Ubuntu、红旗，麒麟••••••

下面来看看期中几个重要的发型版本:

* Redhat： Redhat Linux9.0的内核为2.4.20。在版本9.0后，Redhat不在遵循GPL协议，成为收费产品\(但仍开源\)，发展的新版本一次为Redhat3.x、Redhat4.x、Redhat5.x、Redhat6.x、Redhat7.x、Redhat Enterprise6.x。
* Fedora: 为Redhat的一个分支，仍遵循GPL协议，可以认为是Redhat预发布版。\(就像是游戏的公测版\)
* CentOS\(community Enterprise Operating System\)：与Redhat做到二进制级别的一模一样，Redhat的另一个重要分支，以Redhat所发布的源代码重建符合GPL许可协议的Linux系统，即将Redhat Linux源代码的商标Logo以及非自由软件部分去除在编译而成的版本，目前CentOS已被Redhat公司收购，但仍开源免费，CentOS Linux是国内互联网公司使用最多的Linux系统版本，也是本书的"主人公"，本书后面所有的内容讲解都是基于CentOS这个操作系统的，绝大部分内容几乎无需任何修改同样适合其他操作系统版本。

##### 提示：有关Linux操作系统，记住Redhat、CentOS、Ubuntu、Fedora、SUSE、Debian等即可。 {#提示：有关linux操作系统，记住redhat、centos、ubuntu、fedora、suse、debian等即可。}



#### 

#### Linux发行版本应用场景

Linux发行版本选择

Linux桌面系统 Ubuntu\(开发人员开发平台\)

服务器端Linux系统 首选Redhat\(有钱任性\)或者CentOS

如果对安全要求很高 Debian或FreeBSD

使用数据库高级服务或电子邮件网路哦用户 SUSE

想新技术，新功能是RHEL和CentOS的测试版或预发布版 Fedora

Fedora=稳定之后=&gt;Redhat=去Logo去除收费=&gt;CentOS

中文 红旗Linux，中标麒麟Linux

#### 选择CentOS Linux版本

本诉讲解的Linux运维技术主要是基于CentOS x86\\_64 Linux的，绝大部分知识几乎无需任何修改同样适用于Redhat Linux等同源或类似Linux系统版本。

下面是CentOS的主流版本在国内互联网企业的使用现状说明：

1. CentOS 5系列：占25%左右，主流版本有CentOS 5.5 、CentOS 5.8、CentOS 5.10、CentOS 5.11，不推介新手学习了。=
   &gt;
   Linux kernrl 2.4
2. CentOS 6系列：占45%左右，主流版本有CentOS 6.2、CentOS 6.4、CentOS 6.6、CentOS 6.8，推介新手学习。=
   &gt;
   Linux kernrl 2.6
3. CentOS 7系列：最新的系统，目前正式使用的企业不多，因此不建议去玩它，最好学习目前企业使用较多的6系列，等过2年企业都上了CentOS7的系统，就可以轻松转过去了，不要盲目选择较高的版本。

##### 小面试题：你们公司服务器使用的版本系统是什么？ {#小面试题：你们公司服务器使用的版本系统是什么？}

##### CentOS 6.8 X86\_64 内核版本3.6.32 {#centos-68-x8664-内核版本3632}

##### 面试技巧：大家被面试官问及使用什么样操作系统时，一定要一次性说出来\(系统版本、内核版本、32位和64位\)，例如：我们工作中使用的是CentOS 6.7 x86\_64位Linux系统，内核版本为2.6.32-573，这才是一个合格的Linux运维人员的表现。 {#面试技巧：大家被面试官问及使用什么样操作系统时，一定要一次性说出来系统版本、内核版本、32位和64位，例如：我们工作中使用的是centos-67-x8664位linux系统，内核版本为2632-573，这才是一个合格的linux运维人员的表现。}



