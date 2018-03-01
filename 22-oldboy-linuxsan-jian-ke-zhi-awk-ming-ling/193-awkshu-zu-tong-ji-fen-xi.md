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



10.3 awk数组说明

1、shell与awk中变量默认值为空

2、kuang\[a\] kuang\[b\] kuang\[c\] 中的a、 b、c 被认为是变量，都没有赋值，默认为空

所以 kuang\[a\] kuang\[b\] kuang\[c\] 是同一个元素，最终结果相同

3、数组元素名为字符串时必须用"" kuang\["a"\] kuang\["b"\] kuang\["c"\]

4、awk数组中的元素不一定是连续的，这点不同于其他语言的数组

