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
```

```