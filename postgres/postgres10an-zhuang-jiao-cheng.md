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