#### 如何取得/etiantian文件的权限对应的数字内容，如-rw-r--r--为644，要求使用命令取得644这样的数字

\[root@oldboy test\]\# stat /etiantian\|sed -nr 's\#^.\*\\(0\(.\*\)/-.\*$\#\1\#gp'

644

\[root@oldboy test\]\# stat /etiantian \|awk -F "\[0/\]" 'NR==4{print $2}'

644

\[root@oldboy36 test\]\# stat -c %a /etiantian

644

-oldboy-

1.2.1 方法1：

\[root@oldboy ~\]\# touch /etiantian

\[root@oldboy ~\]\# ls -lhi /etiantian

2318 -rw-r--r-- 1 root root 0 4月 3 09:58 /etiantian

\[root@oldboy ~\]\# ls -l /etiantian \|cut -c 2-10\|tr "rwx-" "4210"

420400400

\[root@oldboy ~\]\# ls -l /etiantian \|cut -c 2-10\|tr "rwx-" "4210"\|awk -F "" '{print $1+$2+$3""$4+$5+$6""$7+$8+$9}'

644

1.2.2 方法2：

\[root@oldboy ~\]\# stat /etiantian \|sed -rn '4s\#^.\*\\(0\(.\*\)/-.\*$\#\1\#gp'

644

1.2.3 方法3：

\[root@oldboy ~\]\# stat -c %a /etiantian

644

1.2.4 方法4

\[root@oldboy ~\]\# stat /etiantian \|awk -F "\[0/\]" 'NR==4{print $2}'

644

1.2.5 方法5：

\[root@oldboy ~\]\# stat /etiantian \|sed -n '4p'\|egrep -o "\[1-9\]{3}"

644

curl -s 不显示错误信息

        -I   取协议（http/ftp等）头



\[root@oldboy ~\]\# curl -I www.baidu.com 2&gt;/dev/null \|sed -n '1p'

HTTP/1.1 200 OK

\[root@oldboy ~\]\# curl -s -I www.baidu.com \|sed -n '1p'

HTTP/1.1 200 OK

