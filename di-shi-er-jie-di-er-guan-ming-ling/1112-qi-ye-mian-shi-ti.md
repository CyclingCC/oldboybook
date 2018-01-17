#### 打印轻量级 web 服务的配置文件 nginx.conf 内容的行号及内容，该如何做？

nl nginx.conf（不记录空行行号）

cat -n nginx.conf &lt;==这个最常用。

less -N nginx.conf

vi/vim 文件 然后执行:set nu，:set nonu为取消行号。

grep -n "." /etc/services 对过滤的内容显示行号，想对所有文件显示行号，就得过滤所有内容。“.”表示任意单个字符。

awk '{print NR,$0}' messages \#NR表示行号，$0表示整行内容。

sed = oldboy.log\| sed 'N;s/\n/ /'

