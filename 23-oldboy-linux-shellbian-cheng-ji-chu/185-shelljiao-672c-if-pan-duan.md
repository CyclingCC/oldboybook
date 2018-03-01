#### 1、if单分支条件语句

```
if [ 条件 ]
    then
        指令
fi
或
if [ 条件 ]；then
    指令
fi
```

提示：分号相当于命令换行，上面两种语句等同。

特殊写法if \[ -f "$file1" \];then echo 1;fi

相当于 \[ -f "$file1" \] && echo 1

##### 例子：

1）输入2个数字，比较大小

```
#!/bin/bash

#no1
if [ $# -ne 2 ]
        then
                echo "USAGE $0 num1 num2"
                exit 1
fi
a=$1
b=$2
if [ $a -lt $b ];then
        echo "yes,$a less than $b"
        exit
fi
if [ $a -eq $b ];then
        echo "yes,$a equal $b"
        exit
fi
if [ $a -gt $b ];then
        echo "yes,$a greater than $b"
        exit
fi
```

2）如果/server2/scripts下面有if3.sh就输出if3.sh到屏幕，如果没有自动创建

```
[root@chensiqi1 scripts]# cat chensiqi.sh
#!/bin/bash

path=/server2/scripts
file=if3.sh
if [ ! -d $path ]
    then
        mkdir -p $path
        echo "directory is not exsist!"
fi
if [ ! -f $path/$file ]
    then
        touch $path/$file
        echo "file is not exsist!"
    else
        echo "file is exsist!"
fi
```



