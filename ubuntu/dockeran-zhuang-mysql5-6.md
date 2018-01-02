# docker安装mysql5.6
`由于mysql5.6版本比较老，apt 源已经找不到，所以使用docker安装比较方便`
```shell
sudo apt install docker.io
sudo docker pull mysql:5.6
sudo docker run --name mysql56 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=unionx123 -d mysql:5.6 --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci 
```
