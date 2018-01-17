假如当前目录是如下命令的结果：

\[root@oldboy oldboy\]\# pwd \#==&gt;这是打印当前目录的，最菜的命令了，你该会的。

/oldboy

现在因为需要进入到了/tmp 目录下进行操作，执行的命令如下：

\[root@oldboy oldboy\]\# cd /tmp

\[root@oldboy tmp\]\# pwd

/tmp

操作完毕后，希望快速返回上一次进入的目录，即/oldboy 目录，该如何做呢？（提示：不能用 cd /oldboy 命令呦）

cd - 返回到上一次的工作目录

cd . 当前目录

cd .. 切换到上级目录

cd - 切换到上一次所在目录

cd ~ 切换到家目录

cd 切换到家目录

cd ~oldboy 切换到oldboy家目录

