### 请执行命令取出linux中eth0的IP地址\(请用cut，有能力者也可分别用awk,sed命令答\) {#11-请执行命令取出linux中eth0的ip地址请用cut，有能力者也可分别用awksed命令答}

方法1

ifconfig eth0 \|sed -n '2p'\|cut -d ":" -f2 \|cut -d " " -f1

方法2

ifconfig eth0\|awk -F "\[ :\]+" 'NR==2{print $4}'

方法3

ifconfig eth0\|sed -n 's\#^.\*ddr:\#\#gp'\|sed -n 's\#B.\*$\#\#gp'

方法4

ifconfig eth0 \|sed -nr '2s\#^.\*dr:\(.\*\) Bc.\*$\#\1\#gp'

ifconfig eth0\|sed -rn '2s\#^\[^0-9\]+\(.\*\) Bc.\*$\#\1\#p'

方法5

ifconfig eth0\|grep -Eo "\(\[0-9\]{1,3}.\){3}\[0-9\]{1,3}" \|head -1

方法6

ifconfig eth0 \|grep -Po '\(?&lt;=addr:\)\S+'

处理技巧：

匹配需要的目标\\(获取的字符串如ip\\)前的字符串一般用以.....开头（^.\_）来匹配开头，匹配的结尾写上实际的字符，如："^.\_addr:" 表示匹配 “ inet addr:”

而处理需要的目标后的内容一般在匹配的开头写上实际的字符，而结尾是用以.......结尾\(.\*$\)来匹配

如: Bcast:.\*$ 表示匹配 “Bcast:10.0.0.25 Mask:255.255.255.0”

