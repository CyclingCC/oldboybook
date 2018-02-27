### 一、linux里面安装软件的3方法  

#### 1、yum 安装

   替你下载软件 替你安装  替你解决依赖关系    点外卖 缺少的东西 外卖解决 

* 方便 简单
* 没有办法深入修改

##### 例子：

yum install  -y  tree

#### 2、 rpm安装    

自己下载软件包 自己安装 自己解决依赖       半成品 缺少的东西 自己解决

安装 解决依赖复杂

rpm -ivh  treexxxxxxxxxxx.rpm

#### 3、编译安装

自己下载软件包 自己安装 自己解决依赖       自己做 按照自己口味 按照继续需求

* 自定义
* 过程复杂

备菜-切菜     炒菜    上菜

./configure    make    make install

#### 4、查看一个软件是否安装了

rpm -qa \#显示出系统已经安装了的软件

-q 查询

-a 所有

\[root@oldboyedu42-lnb ~\]\# rpm -qa\|grep tree 

tree-1.5.3-3.el6.x86\_64

\#iptables是否安装了？

\[root@oldboyedu42-lnb ~\]\# rpm -qa \|grep iptables

iptables-ipv6-1.4.7-16.el6.x86\_64

iptables-1.4.7-16.el6.x86\_64

\[root@oldboyedu42-lnb ~\]\# 

\#查询软件包里面的内容

-l list 

\[root@oldboyedu42-lnb ~\]\# rpm -ql tree

/usr/bin/tree

/usr/share/doc/tree-1.5.3

/usr/share/doc/tree-1.5.3/LICENSE

/usr/share/doc/tree-1.5.3/README

/usr/share/man/man1/tree.1.gz

\[root@oldboyedu42-lnb ~\]\# which tree

/usr/bin/tree

#### 5、 Linux里面常用的工具（yum安装的）

tree  lrzsz  nmap nc  dos2unix 

