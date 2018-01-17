查看一下服务器上是否有运行NetworkManeger 的服务，这个服务会影响到您的网络，可以使用service NetworkManager status ,查看一下服务状态，如果是开启的，请使用stop命令停止，停止后还需要重启网卡服务，service network restart ；如果没有开启继续排查其他问题；

