shell 是命令解释器，它在操作系统的最外层，负责直接与用户对话，把用户的输入解释给操作系统，并处理各种各样的操作系统的输出结果，输出屏幕返回给用户。

#### 1.1.1 交互方式 {#111-交互方式}

1）交互的方式：从键盘输入命令，通过/bin/bash 解析，可以立即得到shell的回应

2）非交互的方式：脚本

#### 1.1.2 Shell 执行命令分为两种方式： {#112-shell-执行命令分为两种方式：}

1）内置命令：讲过的cd ，pwd， exit 和echo 等命令，当用户登陆系统后，shell 以及内置命令就会被系统载入到内存，并且一直运行。

2）一般命令：如ls, 磁盘上的程序文件——》调入内存——》执行命令

![](https://www.luffycity.com/linux-book/assets/22-1.png)

### 1.2 什么是Shell脚本 {#12-什么是shell脚本}

当linux命令或语句不在命令行下执行（严格说，命令行也是shell）而是通过一个程序文件执行时，该程序就被称为Shell 脚本或shell 程序。

用户可以在shell 脚本中敲入一系列的命令及命令语句组合。这些命令，变量和流程控制语句等有机会的结合起来就形成一个功能强大的Shell脚本。

#### 注意事项： {#注意事项：}

1）有没有脚本放在统一的目录

2）权限：用哪个用户执行文件

3）清空文件怎么办，该怎么办

4）错误提示：有没有成功知不知道

5）脚本通用性

![](https://www.luffycity.com/linux-book/assets/22-11.png)

### 1.3 shell脚本在运维工作中的作用地位 {#13-shell脚本在运维工作中的作用地位}

shell脚本擅长处理纯文本类型的数据，而linux中几乎所有配置文件、日志文件等都是纯文本类型文件。
