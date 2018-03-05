#### 1、/etc/skel目录 {#123-etcskel目录}

新用户的老家的默认的样子，从/etc/skel目录复制过来

/etc/skel 目录是用来存放新用户环境变量文件的目录，当我们添加新用户时，这个目录下的所有文件会自动被复制到新添加的用户的家目录下

默认情况下，/etc/skel 目录下的所有文件都是隐藏文件（以点开头的文件）;通过修改、添加、删除/etc/skel目录下的文件，我们可为新创建的用户提供统一的、标准的、初始化用户环境（给所有新用户的一个家默认样子）

#### 企业面试案例：请问如下登录环境故障的原理及解决办法？ {#124-企业面试案例】：请问如下登录环境故障的原理及解决办法？}

-bash-4.1$

-bash-4.1$

假设切换到alex888

-bash-4.1$

-bash-4.1$

\[alex888@oldboyedu35-nb ~\]$

\[alex888@oldboyedu35-nb ~\]$

第一个里程碑-模拟环境

useradd alex888

su - alex888

whoami

\rm -f .bash\*

第二个里程碑-xshell新建一个窗口-并切换到alex888用户

\[root@oldboyedu35-nb ~\]\# su - alex888

-bash-4.1$ whoami

alex888

第三个里程碑-解决故障

\#\#拷贝 /etc/skel 模板中的内容 到 当前用户家目录

-bash-4.1$ cp /etc/skel/.bash\* ~

-bash-4.1$ ll -a

total 20

drwx------ 2 alex888 alex888 4096 Apr 5 10:06 .

drwxr-xr-x. 9 root root 4096 Apr 5 09:22 ..

-rw-r--r-- 1 alex888 alex888 18 Apr 5 10:06 .bash\_logout

-rw-r--r-- 1 alex888 alex888 176 Apr 5 10:06 .bash\_profile

-rw-r--r-- 1 alex888 alex888 124 Apr 5 10:06 .bashrc

第四个里程碑-检查-重新登录

\[root@oldboyedu35-nb ~\]\# su - alex888

\[alex888@oldboyedu35-nb ~\]$ whoami

alex888

/etc/skel 的企业场景作用：

1）可以把想通知的内容放到skel，让登录的人去看

2）统一初始化新用户的环境变量（所有新用户的模板）

3）面试题，linux命令行出现-bash-4.1$问题原因及解决方法

知识点：export PS1='\[\u@\h \W\t\]$' \#\#临时生效

#### 练习题： {#125-etcdefaultuseradd-文件}

1、企业面试案例：请问如下登录环境故障的原理及解决办法？

-bash-4.1$

-bash-4.1$

假设切换到alex888

-bash-4.1$

-bash-4.1$

2、与用户相关的目录是什么？





