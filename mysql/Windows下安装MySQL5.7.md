1.mysql安装目录下的my-default.ini修改成如下

```
basedir ="D:\\engine\\mysql-5.7.16-winx64\\"
datadir ="D:\\engine\\mysql-5.7.16-winx64\\data"
port = 3306
```

2.使用管理员权限打开dos窗口，进入到目录\[必须进入\]bin目录下，执行下面的命令初始化数据库

```dos
mysqld --initialize --user=mysql --console
```

3.安装windows服务

```dos
mysqld --install MySQL
```

4.如果安装失败有问题，可以使用下面的命令删除服务

```dos
mysqld --remove MySQL
```

5.如果初始化的时候，没有记住root的初始化密码，使用下面的命令登录

```dos
#关闭mysql服务
net start mysql
#使用不查表模式，启动服务
mysqld --skip-grant-tables
```

6.使用下面的命令，修改root密码

```sql
use mysql
update user set authentication_string=password('new_password') where user='root' and Host = 'localhost';
#进入之后在修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```



