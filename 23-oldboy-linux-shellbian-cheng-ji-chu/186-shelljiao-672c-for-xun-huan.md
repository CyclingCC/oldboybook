#### 一、循环（for、while）

#### 1、循环语句语法

##### 1）while条件语句

```
while 条件
    do
        指令
done
```

##### 2）for循环结构语法

```
for 变量名 in 变量取值列表
    do
        指令...
done
```

#### 2、while语句

##### 休息命令：sleep 1 休息一秒，usleep 1000000休息1秒单位微妙

1）守护进程

```
[root@oldboy scripts]# cat oldboy.sh 
#!/bin/bash
while true
do
    uptime >> /var/log/uptime.log
    sleep 2
done
```

\#while true 表示条件永远为真，因此会一直运行，像死循环一样。

```
[root@oldboy scripts]# cat /var/log/uptime.log 
 23:01:57 up  8:33,  2 users,  load average: 0.04, 0.03, 0.05
 23:01:59 up  8:33,  2 users,  load average: 0.04, 0.03, 0.05
 23:02:01 up  8:33,  2 users,  load average: 0.04, 0.03, 0.05
```

2）从1加到100

```
[root@oldboy scripts]# cat oldboy.sh 
#!/bin/bash
i=1
sum=0
while [ $i -lt 100 ]
do
    ((sum=sum+i))
    ((i++))
done
echo $sum
```

3）倒计时

```
[root@oldboy scripts]# cat oldboy.sh 
#!/bin/bash

i=10
while [ $i -gt 0 ]
do
    echo $i
    sleep 1
    ((i--))
done
```

#### 3、防止脚本执行中断的方法

1）sh while01.sh & \#放在后台执行

2）screen 分离 ctrl+a+d 查看screen -ls进入screen -r num

3）nohup while01.sh &

#### 4、for循环语句

1）打印列表元素

    [root@oldboy scripts]# cat oldboy.sh 
    #!/bin/bash

    for i in 5 4 3 2 1   #用空格隔开
    do
        echo $i
    done
    [root@oldboy scripts]# sh oldboy.sh 
    5
    4
    3
    2
    1
    [root@oldboy scripts]# for i in {5..1};do echo $i;done
    5
    4
    3
    2
    1
    [root@oldboy scripts]# echo 10.1.1.{1..10}
    10.1.1.1 10.1.1.2 10.1.1.3 10.1.1.4 10.1.1.5 10.1.1.6 10.1.1.7 10.1.1.8 10.1.1.9 10.1.1.10
    [root@oldboy scripts]# for i in `seq 5 -1 1`;do echo $i;done
    5
    4
    3
    2
    1
    #循环执行命令n次
    [root@oldboy scripts]# for i in `seq 100`;do curl -I baidu.com;done

2）开机启动项优化

    [root@oldboy scripts]# cat oldboy.sh 
    #!/bin/bash

    LANG=en
    for i in `chkconfig --list|grep "3:on"|awk '{print $1}'`
    do
        chkconfig $i off
    done

    for name in sshd rsyslog crond network sysstat
    do
        chkconfig $name on
    done

3）在/oldboy目录批量创建文件

    [root@oldboy scripts]# cat oldboy.sh 
    #!/bin/bash
    Path=/oldboy
    [ -d "$Path" ] || mkdir -p $Path
    for i in `seq 10`
    do
        touch $Path/oldboy_$i.html
    done

4）批量改名

    [root@oldboy scripts]# cat oldboy.sh 
    #!/bin/bash
    $Path=/oldboy
    [ -d "$Path" ] || mkdir -p $Path
    for file in `ls $Path`
    do
        mv $file `echo $file|sed -r 's#oldboy(.*).html#linux\1.HTML#g'`
    done

5）批量创建用户并设置密码

    [root@oldboy scripts]# cat oldboy.sh 
    #!/bin/bash

    User=oldboy
    Path=/tmp

    for user in ${User}{01..10}
    do
        useradd $user >/dev/null 2>&1
        if [ ! $? -eq 0 ];then
            echo "$user created faile!"
            echo "scripts begin to rollback!"
            for i in ${User}{01..10}
            do
                userdel -r $i >/dev/null 2>&1
                [ $? -eq 0 ] || exit 1
            done
            echo >$Path/user_passwd
            exit 1
        else
            passWD=`echo $RANDOM|md5sum|cut -c1-8`
            [ -d $Path ] || mkdir $Path
            echo $passWD | passwd --stdin $user
            echo "$user:$passWD">>$Path/user_passwd
        fi
    done

6）获取当前目录下的目录名做为变量列表打印输出

    [root@oldboy ~]# cat /server/scripts/oldboy.sh
    #!/bin/bash

    Path=`pwd`
    echo $Path
    for filename in `ls`
    do
        [ -d ${Path}/${filename} ] && echo $filename
    done

7）九九乘法表

```
[root@oldboy ~]# cat /server/scripts/oldboy.sh 
#!/bin/bash

for ((i=1;i<10;i++))
do
    for ((j=1;j<=i;j++))
    do
        echo -n "$i * $j = $((i*j))"
        echo -n " "
    done
    echo " "
done
[root@oldboy ~]# sh /server/scripts/oldboy.sh
1 * 1 = 1  
2 * 1 = 2 2 * 2 = 4  
3 * 1 = 3 3 * 2 = 6 3 * 3 = 9  
4 * 1 = 4 4 * 2 = 8 4 * 3 = 12 4 * 4 = 16  
5 * 1 = 5 5 * 2 = 10 5 * 3 = 15 5 * 4 = 20 5 * 5 = 25  
6 * 1 = 6 6 * 2 = 12 6 * 3 = 18 6 * 4 = 24 6 * 5 = 30 6 * 6 = 36  
7 * 1 = 7 7 * 2 = 14 7 * 3 = 21 7 * 4 = 28 7 * 5 = 35 7 * 6 = 42 7 * 7 = 49  
8 * 1 = 8 8 * 2 = 16 8 * 3 = 24 8 * 4 = 32 8 * 5 = 40 8 * 6 = 48 8 * 7 = 56 8 * 8 = 64  
9 * 1 = 9 9 * 2 = 18 9 * 3 = 27 9 * 4 = 36 9 * 5 = 45 9 * 6 = 54 9 * 7 = 63 9 * 8 = 72 9 * 9 = 81 
```

#### 5、各种语句小结

1）while循环的特长是执行守护进程以及我们希望循环不退出持续执行，用于频率小于1分钟循环处理（crond），其他的while循环几乎都可以被for循环替代。

2）case语句可以被if语句替换，一般在系统启动脚本传入少量固定规则字符串用case语句，其他普通判断多用if

3）一句话，if，for语句最常用，其次while（守护进程），case（服务启动脚本）

#### 6、获取随机数的几种方法

1）通过系统环境变量$RANDOM

```
[root@oldboy ~]# echo $RANDOM
6178
[root@oldboy ~]# echo $RANDOM
30890
[root@oldboy ~]# echo $((RANDOM%9)) #输出0～9之间随机数
2
[root@oldboy ~]# echo $((RANDOM%9)) 
[root@oldboy ~]# echo $((RANDOM%9))$((RANDOM%9)) #输出00～99 随机数
64
[root@oldboy ~]# echo $((RANDOM%9))$((RANDOM%9)) #输出00～99岁?随机数
10
[root@oldboy ~]# echo $((RANDOM%9))$((RANDOM%9)) #输出00～99岁?随机数
51
[root@oldboy ~]# echo $RANDOM|md5sum #随机数长短不一，可以用md5sum命令统一格式化
599e328a94329684ce5c92b850d32f26  -
```

2）通过openssl产生

```
[root@oldboy ~]# openssl rand -base64 8
aND8WMRM6vQ=
[root@oldboy ~]# openssl rand -base64 8
RsRdRq/9vi4=
[root@oldboy ~]# openssl rand -base64 8|md5sum
b1108cafbc2291392e41d2c914360138  -
[root@oldboy ~]# openssl rand -base64 10      
1frkA2kIJODxqQ==
```

3）通过时间获得随机数

```
[root@oldboy ~]# echo $(date +%N)
361599138
[root@oldboy ~]# echo $(date +%N)
199271856
[root@oldboy ~]# echo $(date +%t%N)
950526316
[root@oldboy ~]# echo $(date +%t%N)
340140329
```

4）urandom

```
[root@oldboy ~]# head /dev/urandom | cksum
621330951 2535
[root@oldboy ~]# head /dev/urandom | cksum
404398617 2470
```

5）UUID

```
[root@oldboy ~]# cat /proc/sys/kernel/random/uuid
8a6c5bbe-2d42-44ac-9ef1-3e7683a613e3
[root@oldboy ~]# cat /proc/sys/kernel/random/uuid
c828c209-5b5f-4bc7-917c-678ed4215988
[root@oldboy ~]# uuidgen
961dc354-81b2-4564-9b85-6095ed4bc7b5
```

#### 7、循环中的三个关键词

##### break continue exit return

##### break continue exit用于循环结构中控制虚幻（for,while,if）的走向





