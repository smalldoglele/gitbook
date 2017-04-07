* 数据库备份

```
#mongodump -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -o 文件存在路径
mongodump -h 192.168.1.254 -d detect_report_test -o d:/dbackup/
#备份成一个文件 使用--gzip 压缩体积会小一点
mongodump -h 192.168.1.53  -d edu20160723 --archive=d:/dbackup/edu.20161223.gz --gzip
```
* 数据库备份到一个文件中(官方实例)
```
mongodump --archive=test.20150715.gz --gzip --db test
```

* 数据还原

```
mongorestore -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 (--drop) 文件存在路径
#还原一个文件
mongorestore -h 101.200.168.176  -d edu20160723 --archive=d:/dbackup/edu.20161223.gz --gzip
```
* 数据还原用一个文件（官方实例）
```
mongorestore --gzip --archive=test.20150715.gz --db test
```
* 删除\(当前\)数据库

```
db.dropDatabase()
```

* 复制数据库

```dos
db.copyDatabase(<from_dbname>,<to_dbname>,<from_hostname>,<username>,<password>);
```

* 数据导出

```
# mongoexport -h 地址 -d 数据库名 -c 集合名 -q 查询条件(json格式) -o 文件地址
mongoexport -h 192.168.1.254 -d detect_report_dev -c detectIndex 
-q {projectName:'硫酸脱氢表雄甾酮'} -od:/data.txt
```

* 数据导入

```
# mongoimport -h 地址 -d 数据库名 -c 集合名  文件地址
mongoimport -h 192.168.1.254 -d detect_report_test -c detectIndex  d:/data.txt
#以csv第一行为表头导入数据
mongoimport h 192.168.1.254 -d "dip_test" -c "user" --file D:\dbackup\user.csv 
--type csv --headerline
```



