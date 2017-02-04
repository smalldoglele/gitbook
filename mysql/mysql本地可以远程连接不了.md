+ 刚安装mysql服务器，使用远程管理工具总是连接不上，于是使用telnet连接这个端口，
```
telnet 192.168.1.10 3306
```
+ 将防火墙关掉
```
service iptables stop
```
通过netstat查看3306的端口状态
```
netstat -apn|grep 3360
```

+ 找到了解决办法
> 修改mysql的配置文件/etc/mysql/my.conf
> 将bind-address后面增加远程访问IP地址或者修改成0.0.0.0

+ 重启mysql服务
```
service mysql restart
```