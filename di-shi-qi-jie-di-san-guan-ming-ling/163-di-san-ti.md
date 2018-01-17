#### 查找当前目录下所有文件，并把文件中的www.etiantian.org字符串替换成www.oldboy.cc

\[root@xdz test\]\# mkdir a/{b,c/d} -pv

mkdir: created directory \`a'

mkdir: created directory \`a/b'

mkdir: created directory \`a/c'

mkdir: created directory \`a/c/d'

\[root@xdz test\]\# tree

.

├── a

│ ├── b

│ └── c

│ └── d

└── oldboy.log

4 directories, 1 file

\[root@xdz test\]\# touch a/aa.txt a/b/bb.txt a/c/cc.txt a/c/d/dd.txt

\[root@xdz test\]\# tree

.

├── a

│ ├── aa.txt

│ ├── b

│ │ └── bb.txt

│ └── c

│ ├── cc.txt

│ └── d

│ └── dd.txt

└── oldboy.log

4 directories, 5 files

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/aa.txt

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/b/bb.txt

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/c/cc.txt

\[root@xdz test\]\# echo "www.etiantian.org" &gt; a/c/d/dd.txt

方法1:

find + \|xargs sed

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f \|xargs cat

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f \|xargs sed 's\#www.etiantian.org\#www.oldboy.cc\#'

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc

方法2：

find + -exec sed

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f -exec cat {} \;

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# find /oldboy/ -type f -exec sed 's\#www.etiantian.org\#www.oldboy.cc\#' {} \;

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc

方法3：

sed + $\(\)

\[root@oldboy36 oldboy\]\# cat $\(find /oldboy/ -type f\)

www.etiantian.org

www.etiantian.org

www.etiantian.org

\[root@oldboy36 oldboy\]\# sed 's\#www.etiantian.org\#www.oldboy.cc\#' $\(find /oldboy/ -type f\)

www.oldboy.cc

www.oldboy.cc

www.oldboy.cc

