#### 已知/oldboy/ett.txt文件内容为：

#### oldboy

#### olldboooy

#### test

#### 请使用grep或egrep正则匹配的方式过滤出前两行内容

\[root@oldboy ~\]\# grep -v "^$" ett.txt

oldboy

xizi

xiaochao

\[root@oldboy ~\]\# sed "/^$/d" ett.txt

oldboy

xizi

xiaochao

\[oldboy@oldboy ~\]$ cat a.txt

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# cat ett.txt

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# grep -v "^o" ett.txt \#→排除以o开头的内容

test

\[root@oldboy oldboy\]\# grep "^o" ett.txt \#→过滤以o开头的内容

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "y$" ett.txt \#→排除以y结尾的内容

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol." ett.txt \#→.代表任意字符

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol.\*" ett.txt \#→\*表表示重复前一个字符1次或多次，.\*结合匹配所有字符。

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol{0,1}" ett.txt \#→重复前一个字符0-1次

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol{5,6}" ett.txt \#→重复前一个字符l,5-6次

\[root@oldboy oldboy\]\# grep "ol{0}" ett.txt \#→重复前一个字符l,正好0次

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\[db,ldboo\]" ett.txt

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "ol\[dbldboo\]" ett.txt

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "\[^test\]" ett.txt \#→过滤出不包含test的内容，此处^和以。。。开头不同。

oldboy

olldboooy

\[root@oldboy oldboy\]\# grep "\[^t\]" ett.txt

oldboy

olldboooy

test

\[root@oldboy oldboy\]\# grep "^\[^t\]" ett.txt \#→过滤出不以t开头的内容

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.bo...y' a.txt

\[oldboy@oldboy ~\]$ grep 'ol.bo\*y' a.txt

oldboy

\[oldboy@oldboy ~\]$ grep 'bo\*y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo.\*y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo...y' a.txt

\[oldboy@oldboy ~\]$ grep 'bo{2,3}y' a.txt

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo{1,3}y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol{1,2}dbo{1,3}y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo\*y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'bo.\*y' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.\*d' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ grep 'ol.d' a.txt

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol+d' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol?d' a.txt

oldboy

\[oldboy@oldboy ~\]$ egrep 'ol+?d' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)y' a.txt

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)oy' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ echo ollldboooooy &gt;&gt;a.txt

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)oy' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol\(db\|ldbo+?\)\*oy' a.txt

oldboy

olldboooy

\[oldboy@oldboy ~\]$ egrep 'ol?d' a.txt

oldboy

\[oldboy@oldboy ~\]$ egrep 'ol+d' a.txt

oldboy

olldboooy

ollldboooooy

\[root@oldboy /data\]\# egrep "ol+dbo+y" /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# sed -n '/ol+dbo+y/p' /oldboy/ett.txt

\[root@oldboy /data\]\# sed -nr '/ol+dbo+y/p' /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# awk '/ol+dbo+y/' /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# egrep "ol+dbo+y" /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# sed -nr '/ol+dbo+y/p' /oldboy/ett.txt

oldboy

olldboooy

\[root@oldboy /data\]\# awk '/ol+dbo+y/' /oldboy/ett.txt

oldboy

olldboooy

