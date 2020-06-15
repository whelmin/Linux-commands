# network 查看网络信息

Netstat 命令用于显示各种**网络信息**，如网络连接，路由表，接口状态 (Interface Statistics)，masquerade 连接，多播成员 (Multicast Memberships) 等等。

## netstat

**语法：**

* -a (all)显示所有选项，默认不显示LISTEN相关
* -t (tcp)仅显示tcp相关选项
* -u (udp)仅显示udp相关选项
* -n 拒绝显示别名，能显示数字的全部转化成数字。
* -l 仅列出有在 Listen (监听) 的服務状态

* -p 显示建立相关链接的程序名
* -r 显示路由信息，路由表
* -e 显示扩展信息，例如uid等
* -s 按各个协议进行统计
* -c 每隔一个固定时间，执行该netstat命令。 持续输出 netstat 信息

找出运行在指定端口的进程

```
$ netstat -an | grep '3000'           // 查看3000端口的服务是否正常启动了
```