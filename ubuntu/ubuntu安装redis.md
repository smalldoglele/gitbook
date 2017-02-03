`对照ubuntu源中的版本是否是官网最新版，一般源里面的redis版本比较老,所以才需要编译安装`
[redis官网下载](https://redis.io/download)

+ 进入到usr文件夹中
```
$ wget http://download.redis.io/releases/redis-X.X.X.tar.gz
$ tar xzf redis-3.2.7.tar.gz
$ cd redis-3.2.7
$ make
```
+ 安装redis为Ubuntu服务
```
./utils/install_server.sh
```


