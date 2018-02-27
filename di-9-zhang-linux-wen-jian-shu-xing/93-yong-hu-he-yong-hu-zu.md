#### 1、对于一个文件来说用户分类

  主人    家人    陌生人 

UID 与 GID 

UID 表示 user  id  用户的id   身份证号码 

GID 表示 group id  用户组的id 户口本号码  

#### 2、系统中的用户分类

1）root    超级管理员  皇帝             0      

2）傀儡用户 虚拟用户                  1-499   

是为了满足linux每个运行的进程都要有一个对应的用户和用户组，无法登录系统的\*\*\*\*\*\*

3）普通用户            百姓 布衣      500+    

#### 3. 与用户有关的文件 

/etc/passwd  用户的信息

/etc/shadow  用户的密码和密码信息

/etc/group   用户组的信息

/etc/gshadow 用户组密码和密码信息

#### 4、/etc/passwd  用户的信息                  

root   :x              :0  :0     :root     :/root          :/bin/bash

oldboy :x              :500:500:            :/home/oldboy  :/bin/bash

alex   :x              :501:501:            :/home/alex     :/bin/bash

用户名 :存放密码的位置   :UID:GID  :用户说明  :用户的家目录   :用户使用的shell\(命令解释器\)

/bin/bash     \#\#\#默认的命令解释器

/sbin/nologin \#\#\#这个用成为了虚拟用户（傀儡用户）

删除存放密码中的x就等同于把密码也删了

