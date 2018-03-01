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

#### 2、if双分支条件语句

```
if [ 条件 ]
    then
        指令
    else
        指令
fi
```

特殊写法：if \[ -f "$file1" \];then echo 1;else echo 0;fi

相当于\[ -f "file1" \] && echo 1 \|\|echo 0

##### 例子：

1）如果/server2/scripts下面有if3.sh就输出if3.sh到屏幕，如果没有就自动创建

    [root@oldboy scripts]# cat chensiqi.sh 
    #!/bin/bash

    file=/server2/scripts/if3.sh
    path=`dirname $file`

    if [ -f $file ];then
        cat $file
        exit 0
    else
        if [ ! -d $path ];then
            mkdir -p $path
            echo "$path is not exist,already created it."
            echo "1234" >> $file
        fi
        if [! -f $file ];then
            echo "1234" >> $file
            echo "$file is not exist,already created it."
        fi
    fi

#### 3、多分支if语句

```
if [ 条件1 ]；then
    指令1
elif [ 条件2 ]；then
    指令2
elif [ 条件3 ]；then
    指令3
elif [ 条件4 ]；then
    指令4
else
    指令n
fi
```

##### 例子：

1）判断两个整数大小

    [root@oldboy scripts]# cat chensiqi.sh 
    #!/bin/bash

    if [ $# -ne 2 ];then
        echo "USAGE $0 num1 num2"
        exit 1
    else
        num1=`echo $1 | sed 's#[0-9]##g'`
        num2=`echo $2 | sed 's#[0-9]##g'`
    fi


    if [ ${#num1} -eq 0 -a ${#num2} -eq 0 ];then
        if [ $1 -lt $2 ];then
            echo "$1 less than $2!"
            exit
        elif [ $1 -eq $2 ];then
            echo "$1 equal $2!"
            exit
        else    
            echo "$1 great than $2!"
            exit
        fi
    else
        echo "num1 num2 must be digit!"
    fi



