* #### Window 下安装

1.服务安装

```bash
#安装服务
 mongod --bind_ip 0.0.0.0 --logpath "F:\MongoDB\db\mongodb.log" --logappend  --dbpath "F:\MongoDB\db" --port 27017 --serviceName "MongoDB" --serviceDisplayName "MongoDB" -- install
 #如果需要加权限加入参数 --auth
```

2.服务操作

```bash
#启动服务
net start MongoDB
#停止服务器
net stop MongoDB
#删除服务
sc delete mongodb
```
* ### Ubuntu 16.04 下安装

1.服务安装


[MongoDB官方文档](https://docs.mongodb.com/manual/)
[Ubuntu上安装MongoDB企业版](https://docs.mongodb.com/manual/tutorial/install-mongodb-enterprise-on-ubuntu/)
 
```
#导入包管理系统使用的公钥
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
#ubuntu 16.04 加入源
echo "deb [ arch=amd64,arm64,ppc64el,s390x ] http://repo.mongodb.com/apt/ubuntu xenial/mongodb-enterprise/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-enterprise.list
#重新加载本地包数据库
sudo apt-get update
#安装最新的稳定企业版mongodb
sudo apt-get install -y mongodb-enterprise
#卸载
sudo apt-get purge mongodb-enterprise*
#删除数据库和日志文件
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb
```
2.服务操作
```
#启动服务
sudo service mongod start
#停止服务
sudo service mongod stop
#重启服务器
sudo service mongod restart
```



