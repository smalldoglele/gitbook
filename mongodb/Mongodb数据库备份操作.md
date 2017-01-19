+ 数据库备份

```dos
#mongodump -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -o 文件存在路径
mongodump -h 192.168.1.254 -d detect_report_test -o d:/dbackup/
#备份成一个文件 使用--gzip 压缩体积会小一点
mongodump -h 192.168.1.53  -d edu20160723 --archive=d:/dbackup/edu.20161223.gz --gzip
```
+ 数据还原

```dos
mongorestore -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 (--drop) 文件存在路径
#还原一个文件
mongorestore -h 101.200.168.176  -d edu20160723 --archive=d:/dbackup/edu.20161223.gz --gzip
```
+ 删除(当前)数据库

```dos
db.dropDatabase()
```
+ 复制数据库

```dos
db.copyDatabase(<from_dbname>,<to_dbname>,<from_hostname>,<username>,<password>);
```