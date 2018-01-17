#### 已知文件test.txt内容为： {#101--已知文件testtxt内容为：}

#### test {#test}

#### liyao {#liyao}

#### oldboy {#oldboy}

#### 请给出输出test.txt文件内容时，不包含oldboy字符串的命令 {#请给出输出testtxt文件内容时，不包含oldboy字符串的命令}

#### grep 筛子 想要的不想要的分开 默认筛子中的要 {#102-grep--筛子--想要的不想要的分开---默认筛子中的要}

\[root@oldboy data\]\# cat test.txt

test

liyao

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt

oldboy

\[root@oldboy data\]\# grep "oldboy" test.txt -v

test

liyao

#### 只查看ett.txt文件（共100行）内第20到第30行的内容 {#103-只查看etttxt文件（共100行）内第20到第30行的内容}

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

