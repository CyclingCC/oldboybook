#### awk linux三剑客老大 {#171-awk---linux三剑客老大}

NR 行号

== 等于

$0 整行

\[root@oldboy ~\]\# awk 'NR&gt;19&&NR&lt;31' a.txt

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

seq 50 \|awk 'NR==20,NR==30 {print}'

\[root@oldboy36 ~\]\# awk '!/oldboy/' oldboy.txt

test

liyao

\[root@oldboy data\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2 {print $4}'

10.0.0.30

\[root@oldboy oldboy\]\# ifconfig eth0\|sed -nr 's\#^.\*dr:\(.\*\) B.\*$\#\1\#gp'

192.168.33.128

\[root@oldboy oldboy\]\# ifconfig eth0\|awk -F "\[ :\]+" 'NR==2 {print $4}'

192.168.33.128

