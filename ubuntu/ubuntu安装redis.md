`对照ubuntu源中的版本是否是官网最新版，一般源里面的redis版本比较老,所以才需要编译安装`

[redis官网下载](https://redis.io/download)

+ 进入到usr文件夹中
```
$ wget http://download.redis.io/redis-stable.tar.gz
$ tar xzf redis-stable.tar.gz
$ cd redis-stable
$ make
```
+ 安装redis为Ubuntu服务
```
./utils/install_server.sh
```
+ 启动/关闭/刷新
```
#所有配置可以在redis_6379 脚本中查看
/etc/init.d/redis_6379 restart/start/stop 
```


