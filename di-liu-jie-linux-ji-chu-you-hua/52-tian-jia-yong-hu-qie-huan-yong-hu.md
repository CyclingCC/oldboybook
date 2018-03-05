#### 1、添加用户

linux/unix是一个多用户、多任务的操作系统

* 超级管理员（root）：root默认在unix/linux操作系统中拥有最高的管理权限。比喻：皇帝
* 普通用户：管理员或者具备管理权限的用户创建的。权限：系统管理仅可以读、看，不能增、删、改

权限越大，责任越大

可使用如下命令添加一个普通用户账号，并为其设置口令：

\[root@oldboyedu42 ~\]\# useradd  oldboy

\[root@oldboyedu42 ~\]\# id  oldboy

uid=500\(oldboy\) gid=500\(oldboy\) groups=500\(oldboy\)

\[root@oldboyedu42 ~\]\# id  lilaoshi

id: lilaoshi: No such user

\[root@oldboyedu42 ~\]\# passwd   oldboy   ===&gt;问你新的密码，然后输入 交互设置密码

Changing password for user oldboy.

New password:

BAD PASSWORD: it is too simplistic/systematic  ===&gt;提示密码太简单了，但可以不理会

BAD PASSWORD: is too simple

Retype new password:

passwd: all authentication tokens updated successfully.

##### 提示：

一般情况下，在企业生产环境中应尽量避免直接到root用户下操作，除非有超越普通用户权限的系统维护需求，使用完成后立刻退回普通用户

非交互式设置密码：还可通过下面的命令一步到位地设置密码（其中，oldboy为用户名，密码为123456）

echo "123456" \|passwd --stdin oldboy && history -c

#### 2、切换用户

\[root@oldboyedu44 ~\]\# su - oldboy     ===&gt;由root管理员，切换到普通用户oldboy

\[oldboy@oldboyedu44 ~\]$ whoami        ===&gt;查看当前用户是什么

oldboy

\[oldboy@oldboyedu44 ~\]$ su - root     ===&gt;切回到root用户

Password:

\[root@oldboyedu44 ~\]\# su - oldboy

\[oldboy@oldboyedu44 ~\]$ su

Password:

说明：

* 超级用户root切换到普通用户下面，无需输入对应用户密码，这相当于“皇帝”去“大臣”家里
* 普通用户切换到root或其他普通用户下，需要输入切换的对应用户密码
* 普通用户的权限比较小，只能进行基本的系统信息查看等操作，无法更改系统配置和管理服务
* $符号是普通用户的命令行提示符，\#符号是超级管理员的提示符，示例如下：

![](/assets/6-4.png)

\[root@oldboy ~\]\#       "\#" ===&gt;超级管理员root对应的提示符

\[oldboy@oldboy ~\]$     "$" ===&gt;普通用户oldboy对应的提示符

* 提示符@前面的字符代表当前用户（可用whoami查询），后面的为主机名（可用hostname查询），~所在的位置是窗口当前用户所在的路径。示例如下：

\[oldboy@oldboy ~\]$  ===&gt; oldboy为当前用户，oldboyedu44为主机名，~表示当前目录，即家目录

#### 练习题：

1、如何添加用户

2、如何从root用户切换到普通用户

3、su与su -的区别



