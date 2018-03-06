#### 1、awk数组

awk提供了数组来存放一组相关的值。

awk是一种编程语言，肯定也支持数组的运用，但是又不同于c语言的数组。数组在awk中被称为关联数组，因为它的下标既可以是数字也可以是字符串。下标通常被称作key，并且与对应的数组元素的值关联。数组元素的key和值都存储在awk程序内部的一张表中，通过一定散列算法来存储，所以数组元素都不是按顺序存储的。打印出来的顺序也肯定不是按照一定的顺序，但是我们可以通过管道来对所需的数据再次操作来达到自己的效果。

![](/assets/21-19.png)如图不难发现，awk数组就和酒店一样。数组的名称就像是酒店名称，数组元素名称就像酒店房间号码，每个数组元素里面的内容就像是酒店房间里面的人。

#### 2、图片-数组

假设我们有一个酒店

```
酒店<===>oldboyhotel
```

酒店里面有几个房间110，119，120，114这几个房间

```
酒店110房间<===>oldboyhotel[110]
酒店120房间<===>oldboyhotel[120]
酒店119房间<===>oldboyhotel[119]
酒店114房间<===>oldboyhotel[114]
```

酒店房间里面入住客人

```
酒店110房间住着xiaoyu<===>oldboyhotel[110]="xiaoyu"
酒店119房间住着ruxue<===>oldboyhotel[119]="ruxue"
酒店120房间住着dandan<===>oldboyhotel[120]="dandan"
酒店114房间住着waiwai<===>oldboyhotel[114]="waiwai"
```

例子：

```
[root@oldboy ~]# awk 'BEGIN{oldboyhotel[110]="xiaoyu";oldboyhotel[119]="ruxue";oldboyhotel[120]="dandan";oldboyhotel[114]="waiwai";print oldboyhotel[110],oldboyhotel[119],oldboyhotel[120],oldboyhotel[114]}'
xiaoyu ruxue dandan waiwai
```

```
[root@oldboy ~]# awk 'BEGIN{oldboyhotel[110]="xiaoyu";oldboyhotel[119]="ruxue";oldboyhotel[120]="dandan";oldboyhotel[114]="waiwai";for(hotel in oldboyhotel)print hotel,oldboyhotel[hotel]}'
110 xiaoyu
120 dandan
114 waiwai
119 ruxue
```

企业面试题：统计域名访问次数

处理以下文件内容，将域名取出并根据域名进行计数排序处理：（百度和sohu面试题）

```
http://www.etiantian.org/index.html
http://www.etiantian.org/1.html
http://post.etiantian.org/index.html
http://mp3.etiantian.org/index.html
http://www.etiantian.org/3.html
http://post.etiantian.org/2.html
```

思路：

1）以斜线为菜刀取出第二列（域名）

2）创建一个数组

3）把第二列（域名）作为数组的下标

4）通过类似于i++的形式进行计数

5）统计后把结果输出

过程演示：

第一步：查看一下内容

```
[root@oldboy ~]# awk -F "[/]+" '{print $2}' file 
www.etiantian.org
www.etiantian.org
post.etiantian.org
mp3.etiantian.org
www.etiantian.org
post.etiantian.org
```

命令说明：

这是我们需要计数的内容

第二步：计数

```
[root@oldboy ~]# awk -F "[/]+" '{i++;print $2,i}' file 
www.etiantian.org 1
www.etiantian.org 2
post.etiantian.org 3
mp3.etiantian.org 4
www.etiantian.org 5
post.etiantian.org 6
```

命令说明：

i++:i最开始是空的，当awk读取一行，i自身+1

第三步：用数组替换i

```
[root@oldboy ~]# awk -F "[/]+" '{h[$2]++;print $2,h["www.etiantian.org"]}' file 
www.etiantian.org 1
www.etiantian.org 2
post.etiantian.org 2
mp3.etiantian.org 2
www.etiantian.org 3
post.etiantian.org 3
```

命令说明：

1）将i替换成h\[$2\];相当于我创建了一个数组h\[\]，然后用$2作为我的房间号。但是目前房间里是没有东西的。也就是说h\[$2\]=h\["www.etiantian.org"\] and h\["post.etiantian.org"\] and h\["mp3.etiantian.org"\] 但是具体房间里是没有东西的也就是空。

2）h\[$2\]++就等于i++：也就是说我开始给房间里加东西；当出现同样的东西，我就++

3）print h\["www.etiantian.org"\]:意思就是说我开始要输出了。我要输出的是房间号为“www.etiantian.org”里面的内容。这里面的内容最早是空的，随着awk读取每一行一旦出现房间号为“www.etiantian.org”的房间时，我就给房间里的内容进行++。

4）综上，输出的结果中，每次出现www.etiantian.org时，h\["www.etiantian.org"\]就会++。因此最后的输出数字是3

第四步：输出最终计数结果

```
[root@oldboy ~]# awk -F "[/]+" '{h[$2]++}END{for(i in h)print i,h[i]}' file 
mp3.etiantian.org 1
post.etiantian.org 2
www.etiantian.org 3
```

命令说明：

我们最终需要输出的是去重复以后的统计结果，所以得在END模块里进行输出

for（i in h）遍历这个数组，i里存的都是房间号

print i，h\[i\]：输出每一个房间号及其房间里的内容（计数结果）

提示：

awk的应用里最重要的一个功能就是计数，而数组在awk里最大的作用就是去重复。请同学们仔细理解，多动手试验一下。

#### 练习题：

1、什么是awk数组及数组的结构组成

2、统计域名访问次数

