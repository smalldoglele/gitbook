1.用户登录
```
#格式:mysql -h主机地址 -u用户名 -p用户密码
mysql -h 110.110.110.110 -u root -p 123
#本地可以直接mysql –uroot -p
```
2.用户退出`exit/quit`

3.添加用户
```
#mysql.user表保存的是用户的登录信息
#直接添加无权限
insert into mysql.user (host,user,password) values('%','walden',PASSWORD('password'));
#添加并赋权
grant select on 数据库.* to '用户名'@'登录主机' identified by '密码'
```
4.用户权限
```
#添加权限
####################################################
# 权限:select ,update,delete,insert(表数据)、
# create,alert,drop(表结构)、
# references(外键)、
# create temporary tables(创建临时表)、
# index(操作索引)、
# create view,show view(视图)、
# create routine,alert routine,execute(存储过程)、
# all,all privileges(所有权限)
# 
# 数据库：数据库名或者*(所有数据库)
# 表：表名或者*(某数据库下所有表)
# 主机:主机名或者%(任何其他主机)
####################################################

#grant 权限 on 数据库.表 to '用户名'@'登录主机';
grant selec,insert,update,delete on *.* to 'walden'@'%';
#撤销权限 将to改为from
#revoke 权限 on 数据库.表 from '用户名'@'登录主机';
revoke all on *.* from ‘walden’@’%’;
#查看[自己]权限
show grants;
#查看指定用户[dba]指定host
show grants for dba@localhost;
```
5.删除用户
```
delete from mysql.user where user='' and host='';
```
6.修改密码
```
update mysql.user set password=PASSWORD('123456') where user='root';
```
7.找回密码
```
#关闭mysql服务
kill all -TERM mysqld
```
8.修改配置文件
```
vi /etc/my.cnf
```
```
#在[mysqld]的段中加上一句：skip-grant-tables
[mysqld]
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
skip-grant-tables
```
```
#重启mysqld
service mysqld restart
```
```
#刷新权限
flush privileges;
```

8.远程用户
+ 限制在指定ip登录host为ip详情请看 添加权限
+ 在任意远程ip登录host为%详情请看 添加权限



9.标准实例

1. mysql.user表实例：一般来说，Host字段都使用ip来限制，而不是机器名（机器名可变，不是特别靠谱）
```
select Host, User from user;
```
2. 授权实例：
```
show grants for 'helper'@'110.111.127.%'
```
