#### 1、使用dos2unix处理脚本

从windows编辑的脚本到Linux下需要使用这个命令

dos2unix windows.sh

#### 2、使用echo命令调试

在变量读取或修改的前后假如echo $变量，也可在后面使用exit退出脚本，这样可以不用注释后边代码

#### 3、利用bash的参数调试

sh \[-nvx\]

-n:不会执行该脚本，仅查询脚本语法是否有问题，并给出错误提示。可用于生产服务器那些只能执行一次不可逆的脚本。

-v：在执行脚本时，先将脚本的内容输出到屏幕上然后执行脚本，如果有错误，也会给出错误提示。（一般不用）

-x：将执行的脚本内容及输出显示到屏幕上，常用

#### 4、shell脚本调试技巧小结：

1）要记得首先用dos2unix对脚本格式化

2）直接执行脚本根据报错来调试，有时报错不准确。

3）sh -x调试整个脚本，显示执行过程。

4）set -x和set +x调试部分脚本（在脚本中设置）

5）echo输出变量及相关内容，然后紧跟着exit退出，不执行后面程序的方式，一步步跟踪脚本，对于逻辑错误比较好用。

6）最关键的时语法熟练，编码习惯，编程思想，将错误扼杀在萌芽中，减轻调试负担，提高效率。

#### 练习题：

简述shell脚本调试的技巧

