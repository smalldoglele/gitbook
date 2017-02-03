1.用户登录
```
#格式:mysql -h主机地址 -u用户名 -p用户密码
mysql -h 110.110.110.110 -u root -p 123
#本地可以直接mysql –uroot -p
```
2.用户退出
'exit/quit'
3.添加用户
mysql.user表保存的是用户的登录信息
直接添加无权限
insert into mysql.user (host,user,password) values('%','walden',PASSWORD('walden'));

添加并赋权
grant select on 数据库.* to '用户名'@'登录主机' identified by '密码'

四、        用户权限
添加权限
grant 权限 on 数据库.表 to '用户名'@'登录主机';

权限： select ,update,delete,insert(表数据)、create,alert,drop(表结构)、references(外键)、create temporary tables(创建临时表)、index(操作索引)、create view,show view(视图)、create routine,alert routine,execute(存储过程)、all,all privileges(所有权限)

数据库：数据库名或者*(所有数据库)

表：表名或者*(某数据库下所有表)

主机:主机名或者%(任何其他主机)

例：grant selec,insert,update,delete on *.* to 'walden'@'%';

撤销权限
revoke 权限 on 数据库.表 from '用户名'@'登录主机';//将to改为from

例：revoke all on *.* from ‘walden’@’%’;

查看权限
show grants;//自己

show grants for dba@localhost;//指定用户指定host

五、        删除用户
delete from mysql.user where user='' and host='';

六、        修改密码
update mysql.user set password=PASSWORD('111111') where user='root';

七、        找回密码
关闭mysql服务
killall -TERM mysqld

修改配置文件
vi /etc/my.cnf

在[mysqld]的段中加上一句：skip-grant-tables

例如：

[mysqld]

datadir=/var/lib/mysql

socket=/var/lib/mysql/mysql.sock

skip-grant-tables

重启mysqld
service mysqld restart

登录
mysql -uroot -p

修改密码
update mysql.user set password=PASSWORD('111111') where user='root';

flush privileges;//刷新权限

修改配置文件
 vi /etc/my.cnf

去掉之前的改动

重启服务
设置远程用户
八、        远程用户
①     限制在指定ip登录host为ip详情请看 添加权限

②     在任意远程ip登录host为%详情请看 添加权限

远程访问
mysql -h110.110.110.110 -uroot -p123;//指定h为ip详情请看 用户登录

 

 

一些标准实例：

1. mysql.user表实例：一般来说，Host字段都使用ip来限制，而不是机器名（机器名可变，不是特别靠谱）

select Host, User from user;

| 172.17.% | dev | 
| 172.17.0.% | export | 
| 172.17.0.20 | demo | 
| 172.28.0.% | dev | 
| 192.168.% | dev | 
| 110.111.126.% | demo | 
| 110.111.126.103 | helper          | 
| 110.111.127.% | webnav    | 
| localhost | backup | 
| localhost | backupdata | 
| localhost | root | 
+-----------------+-----------------+

2. 授权实例：show grants for 'helper'@'110.111.127.%'

+--------------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO 'helper'@'110.111.127.%' IDENTIFIED BY PASSWORD 'xxxxxxxxxxxxxxxxx' WITH MAX_USER_CONNECTIONS 200 | 
| GRANT ALL PRIVILEGES ON `helper_online`.* TO 'helper'@'110.111.127.%' | 
+--------------------------------------------------------------------------------------------------------------------------------------------------+