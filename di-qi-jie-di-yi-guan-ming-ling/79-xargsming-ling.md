#### xargs 又称管道命令，构造参数等。是给命令传递参数的一个过滤器,也是组合多个命令的一个工具 它把一个数据流分割为一些足够小的块,以方便过滤器和命令进行处理 。简单的说 就是把 其他命令的给它的数据 传递给它后面的命令作为参数

#### xargs 从标准输入获取内容创建和执行命令

-n 数字 做分组，几个一组 -i {}

\[root@oldboy ~\]\# echo 1 2 3 4 &gt;a.txt

\[root@oldboy ~\]\# cat a.txt

1 2 3 4

\[root@oldboy ~\]\# xargs -n 2 &lt; a.txt

1 2

3 4

\[root@oldboy ~\]\# find /data/ -type d -name "\*.txt"

/data/10.txt

/data/4.txt

/data/8.txt

/data/2.txt

/data/5.txt

/data/6.txt

/data/1.txt

/data/3.txt

/data/9.txt

/data/7.txt

\[root@oldboy ~\]\# find /data/ -type d -name "\*.txt" \|xargs -n 2

/data/10.txt /data/4.txt

/data/8.txt /data/2.txt

/data/5.txt /data/6.txt

/data/1.txt /data/3.txt

/data/9.txt /data/7.txt

