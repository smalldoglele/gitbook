#### ubunut16.04安装postgres10
[官方教程页面](https://www.postgresql.org/download/linux/ubuntu/)
+ 新建postgres源文件
```
/etc/apt/sources.list.d/pgdg.list
```
+ 源文件内容 16.04的postgres文件
```
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
```
+ 下载访问postgres的公钥
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
```
+ 安装postgres 数据库
```
sudo apt-get install postgresql-10
```
+ 数据库数据和日志文件路径
```
/var/lib/postgresql/10/main
/var/log/postgresql/postgresql-10-main.log
```
+ 给linux的postgres用户设置密码
```
sudo passwd postgres
## 输入密码两次
#切换到postgres用户
su postgres 
# 执行
psql
```
+ 给数据库的postgres用户设置密码
```
postgres=# alter user postgres with password 'your_password';
ALTER ROLE
```
+ ### PostgreSQL允许远程访问设置方法

1.修改pg_hba.conf文件，配置用户的访问权限（#开头的行是注释内容）：
```
# TYPE DATABASE  USER    CIDR-ADDRESS     METHOD
# "local" is for Unix domain socket connections only
local all    all               trust
# IPv4 local connections:
host  all    all    127.0.0.1/32     trust
host  all    all    192.168.1.0/24    md5
# IPv6 local connections:
host  all    all    ::1/128       trust
```
其中，第7条是新添加的内容，表示允许网段192.168.1.0上的所有主机使用所有合法的数据库用户名访问数据库，并提供加密的密码验证。

其中，数字24是子网掩码，表示允许192.168.1.0--192.168.1.255的计算机访问
2.修改postgresql.conf文件，将数据库服务器的监听模式修改为监听所有主机发出的连接请求
```
定位到#listen_addresses=’localhost’。PostgreSQL安装完成后，默认是只接受来在本机localhost的连接请 求。

将行开头都#去掉，将行内容修改为listen_addresses=’*'来允许数据库服务器监听来自任何主机的连接请求
```