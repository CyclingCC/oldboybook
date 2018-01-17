### case结构条件句语法 {#111-case结构条件句语法}

![](https://www.luffycity.com/linux-book/assets/22-21.png)

![](https://www.luffycity.com/linux-book/assets/22-22.png)

### 11.2 给指定文本加颜色 {#112-给指定文本加颜色}

echo -e "\033\[30m 黑色字oldboy trainning \033\[0m"

echo -e "\033\[31m 红色字oldboy trainning \033\[0m"

echo -e "\033\[32m 绿色字oldboy trainning \033\[0m"

echo -e "\033\[33m 黄色字oldboy trainning \033\[0m"

echo -e "\033\[34m 蓝色字oldboy trainning \033\[0m"

echo -e "\033\[35m 紫色字oldboy trainning \033\[0m"

echo -e "\033\[36m 天蓝字oldboy trainning \033\[0m"

echo -e "\033\[37m 白色字oldboy trainning \033\[0m"

### 11.3 echo给字符串加不同颜色 {#113-echo给字符串加不同颜色}

#### 11.3.1 直接加颜色 {#1131-直接加颜色}

echo -e "\033\[40;37m 黑底白字 welcome to old1boy\033\[0m"

echo -e "\033\[41;37m 红底白字 welcome to old2boy\033\[0m"

echo -e "\033\[42;37m 绿底白字 welcome to old3boy\033\[0m"

echo -e "\033\[43;37m 黄底白字 welcome to old4boy\033\[0m"

echo -e "\033\[44;37m 蓝底白字 welcome to old5boy\033\[0m"

echo -e "\033\[45;37m 紫底白字 welcome to old6boy\033\[0m"

echo -e "\033\[46;37m 天蓝白字 welcome to old7boy\033\[0m"

echo -e "\033\[47;30m 白底黑字 welcome to old8boy\033\[0m"

