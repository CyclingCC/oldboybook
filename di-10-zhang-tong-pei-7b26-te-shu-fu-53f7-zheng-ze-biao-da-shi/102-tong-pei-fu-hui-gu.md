#### 1、 \*     所有 任何东西

以.txt结尾 \*.txt

以.log结尾 \*.log

系统中以ls开头的文件。

find / -type f -name "ls\*"

找出系统中文件名包含oldboy的文件。

find / -type f  -name "\*oldboy\*"

#### 2、{}  生成序列 

echo {1..10}

echo {10..1}

echo {01..10}

echo {01..100}

echo {a..c}

echo {a..z}

echo {A..Z}

\[root@oldboyedu42-lnb ~\]\# echo stu{01..10}

stu01 stu02 stu03 stu04 stu05 stu06 stu07 stu08 stu09 stu10

\[root@oldboyedu42-lnb ~\]\# echo 20{01..10}

2001 2002 2003 2004 2005 2006 2007 2008 2009 2010

#### \#通过{}

\[root@oldboyedu42-lnb ~\]\# echo {a..z}

a b c d e f g h i j k l m n o p q r s t u v w x y z

\[root@oldboyedu42-lnb ~\]\# echo {a c f}

{a c f}

\[root@oldboyedu42-lnb ~\]\# echo {a,c,f}

a c f

\[root@oldboyedu42-lnb ~\]\# echo A{B,C}

AB AC

\[root@oldboyedu42-lnb ~\]\# echo A{,C}

A AC

\[root@oldboyedu42-lnb ~\]\# echo oldboy.txt{,.bak}

oldboy.txt oldboy.txt.bak

\[root@oldboyedu42-lnb ~\]\# touch oldboy.txt

\[root@oldboyedu42-lnb ~\]\# cp  oldboy.txt{,.bak}

cp: overwrite \`oldboy.txt.bak'? y

\[root@oldboyedu42-lnb ~\]\# ls -l oldboy.txt\* 

\[root@oldboyedu42-lnb ~\]\# ls -l oldboy.txt\* 

-rw-r--r--  3 root root 0 Nov 11 23:50 oldboy.txt

-rw-r--r--. 1 root root 0 Nov 11 23:50 oldboy.txt.bak

-rw-r--r--  3 root root 0 Nov 11 23:50 oldboy.txt-hard

\[root@oldboyedu42-lnb ~\]\# 

\[root@oldboyedu42-lnb ~\]\# \#cp  oldboy.txt{,.bak}

\[root@oldboyedu42-lnb ~\]\# echo   oldboy.txt{,.bak}

oldboy.txt oldboy.txt.bak

\[root@oldboyedu42-lnb ~\]\# echo   A{,C}

A AC

#### 3、小结 

1）查找文件 

2）\*  {}  

3）？ 任何一个

