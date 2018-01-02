# docker安装mysql5.6
`由于mysql5.6版本比较老，apt 源已经找不到，所以使用docker安装比较方便`
```shell
#安装docker
sudo apt install docker.io
#拉取镜像
sudo docker pull mysql:5.6
#安装mysql 5.6 并配置编码
sudo docker run --name mysql56 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=unionx123 -d mysql:5.6 --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci 
# 也可以使用 utf8mb4_unicode_ci
```
