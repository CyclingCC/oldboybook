#### 1、grep命令

##### i、已知文件test.txt内容为：

##### test

##### liyao

##### oldboy

##### 请给出输出test.txt文件内容时，不包含oldboy字符串的命令

##### grep 筛子 想要的不想要的分开 默认筛子中的要

\[root@oldboy data\]\# cat test.txt

test

liyao

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt -v

test

liyao

##### ii、只查看ett.txt文件（共100行）内第20到第30行的内容

\[root@oldboy ~\]\# grep 20 -A 10 a.txt 记忆方法 after

20

21

22

23

24

25

26

27

28

29

30

\[root@oldboy ~\]\# grep 30 -B 10 a.txt 记忆方法 before

20

21

22

23

24

25

26

27

28

29

30

\[root@oldboy ~\]\# grep 25 -C5 a.txt

20

21

22

23

24

25

26

27

28

29

30

#### 2、sed命令

##### i、sed \*\*\*\*\* 擅长取行，替换，linux三剑客老二

sed \[选项\] \[sed命令\] \[输入文件\]

-n 取消默认输出，功能p\(print\)打印

例：取行：sed -n '20,30p' ett.txt

g与s联合使用时，表示对当前行全局匹配替换，s常说的查找并替换，用一个字符串替换成另一个

-e允许多项编辑

-i修改文件内容（修改磁盘上的内容）

##### ii、sed过滤

sed -n '/oldboy/p' test.txt

\[root@oldboy ~\]\# sed -n '20,30p' a.txt

20

21

22

23

24

25

26

27

28

29

30

##### iii、sed替换

\[root@oldboy ~\]\# sed 's\#oldgirl\#gongli\#' a.txt

oldboy gongli

gongli

\#是分隔符，分隔符可以是任意的

##### iv、sed删除

\[root@oldboy data\]\# cat test.txt

test

liyao

oldboy

\[root@oldboy36 ~\]\# sed -n '/oldboy/!p' oldboy.txt

test

liyao

\[root@oldboy36 ~\]\# sed '/oldboy/d' oldboy.txt

test

liyao

##### v、sed修改文件内容

\[root@oldboy ~\]\# sed -i 's\#oldgirl\#gongli\#g' a.txt

\[root@oldboy ~\]\# cat a.txt

oldboy gongli

gongli

#### 3、awk命令



