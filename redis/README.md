##Redis常用操作配置

+ 删除模糊匹配的键值
```
# redis-cli -a 密码 -n 数据库号 keys shiro* | xargs redis-cli -a 密码 -n 数据库号 del
redis-cli -a java2000wl -n 0 keys shiro* | xargs redis-cli -a java2000_wl -n 0 del
```
+ 查看某个键值的超时时间
