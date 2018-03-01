#### 1、数组结构

数组名\\[下标\\] =值

arrayname\[string\]=value

#### 2、awk一些实例

```
[root@nfsserver files]# awk 'BEGIN{man="woman";print man}'
woman
[root@nfsserver files]# awk 'BEGIN{man="woman woman2 woman3";print man}'
woman woman2 woman3
[root@nfsserver files]# awk 'BEGIN{kuang[1]="woman";kuang[2]="woman2";kuang[3]="woman3";print kuang[1],kuang[2],kuang[3]}'
woman woman2 woman3
[root@oldboy36 ~]# awk 'BEGIN{kuang[a]="woman";kuang[b]="woman2";kuang[c]="woman3";print a,kuang[a],b,kuang[b],c,kuang[c]}'
woman3 woman3 woman3
[root@oldboy36 ~]# awk 'BEGIN{kuang["a"]="woman";kuang["b"]="woman2";kuang["c"]="woman3";print a,kuang["a"],b,kuang["b"],c,kuang["c"]}'
woman woman2 woman3
```

#### 3、awk数组说明

1）shell与awk中变量默认值为空

2）kuang\[a\] kuang\[b\] kuang\[c\] 中的a、 b、c 被认为是变量，都没有赋值，默认为空

所以 kuang\[a\] kuang\[b\] kuang\[c\] 是同一个元素，最终结果相同

3）数组元素名为字符串时必须用"" kuang\["a"\] kuang\["b"\] kuang\["c"\]

4）awk数组中的元素不一定是连续的，这点不同于其他语言的数组

#### 4、awk BEGIN模块

BEGIN模块在awk读取文件之前就执行，一般用来定义我们的内置变量（FS,RS等）

可以输出表头（excel表格名称）

BEGIN模块可以做一些测试，如算术运算

\[root@oldboy files\]\# awk 'BEGIN{print 10/3}'

3.33333

#### 5、awk END模块

END在awk读取完所有文件的时候，再执行END模块，一般用来输出一个结果（累加，数组结果），

也可以是和BEGIN模块类似的结尾标识信息

注意 BEGIN或END模块只能有一个

模式{动作} 可以是多个

'NR==2{print $1}NR==5{print $0}'

awk -F ":" 'NR==1{print NR,$0}NR==2{print NR,$NF}' awkfile.txt

