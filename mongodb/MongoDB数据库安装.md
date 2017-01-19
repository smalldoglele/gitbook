#### Window 下安装
1.服务安装
```bash
#安装服务
 mongod --bind_ip 0.0.0.0 --logpath "F:\MongoDB\db\mongodb.log" --logappend  --dbpath "F:\MongoDB\db" --port 27017 --serviceName "MongoDB" --serviceDisplayName "MongoDB" -- install
 #如果需要加权限加入参数 --auth
```
2.服务操作
```bash
#启动服务
net start MongoDB
#停止服务器
net stop MongoDB
#删除服务
sc delete mongodb
```