#### 1、case结构条件句语法

```
case "字符串变量" in
    值1）
        指令1
        ;;
    值2）
        指令2
        ;;
    *)
        指令
esac
```

注意：case语句相当于一个if的多分支结构语句

```
值1的选项
apple）
    echo -e "@RED_COLOR apple $RES"
    ;;
也可以这样写，输入2种格式找同一个选项
apple|APPLE)
    echo -e "$RED_COLOR apple $RES"
    ;;
```

##### case 语句小结

1）case语句就相当于多分支的if语句。case语句的优势是更规范，易读。

2）case语句适合变量的值少，且为固定的数字或字符串集合。

3）系统服务启动脚本传参的判断多用case语句

#### 2、给指定文本加颜色

以传参为例，在脚本命令行传2个参数，给指定内容（第一个参数）加指定颜色（第二个参数）

```
echo -e "\033[30m 黑色字oldboy trainning \033[0m"
echo -e "\033[31m 红色字oldboy trainning \033[0m"
echo -e "\033[32m 绿色字oldboy trainning \033[0m"
echo -e "\033[33m 黄色字oldboy trainning \033[0m"
echo -e "\033[34m 蓝色字oldboy trainning \033[0m"
echo -e "\033[35m 紫色字oldboy trainning \033[0m"
echo -e "\033[36m 天蓝字oldboy trainning \033[0m"
echo -e "\033[37m 白色字oldboy trainning \033[0m"
```

#### 3、echo给字符串加不同颜色

```
echo -e "\033[40;37m 黑底白字 welcome to old1boy\033[0m"
echo -e "\033[41;37m 红底白字 welcome to old2boy\033[0m"
echo -e "\033[42;37m 绿底白字 welcome to old3boy\033[0m"
echo -e "\033[43;37m 黄底白字 welcome to old4boy\033[0m"
echo -e "\033[44;37m 蓝底白字 welcome to old5boy\033[0m"
echo -e "\033[45;37m 紫底白字 welcome to old6boy\033[0m"
echo -e "\033[46;37m 天蓝白字 welcome to old7boy\033[0m"
echo -e "\033[47;30m 白底黑字 welcome to old8boy\033[0m"
```

#### 练习题：

1、写出case语句的格式



