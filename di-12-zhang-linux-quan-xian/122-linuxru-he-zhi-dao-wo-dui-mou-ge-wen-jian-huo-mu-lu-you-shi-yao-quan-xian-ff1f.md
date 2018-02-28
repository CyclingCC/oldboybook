#### 1、权限安全临界点

inux的默认权限就是安全的临界点，也是最佳的权限

目录 755  文件 644  是 相对安全的临界点

用户为root  用户组为root

![](/assets/18-3.png)

1、http协议 请求方法控制post，禁止get

2、挂载  noexec

3、程序前端控制 .jpg,zip

4、服务层，指定目录禁止php解析

![](/assets/18-4.png)

