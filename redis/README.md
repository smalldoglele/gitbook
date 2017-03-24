##Redis常用操作配置

+ 删除模糊匹配的键值
```
# redis-cli -a 密码 -n 数据库号 keys shiro* | xargs redis-cli -a 密码 -n 数据库号 del
redis-cli -a java2000wl -n 0 keys shiro* | xargs redis-cli -a java2000_wl -n 0 del
```
+ 查看某个键值的超时时间
    
    1.TTL 命令
    
    > Redis TTL 命令以秒为单位返回 key 的剩余过期时间
    > TTL KEY_NAME
    >　　返回值的意义
    > -2：key不存在
    > -1：存在，但未设置剩余生存时间
    > 否则，以秒为单位返回key的生存时间。
    
    2.Redis Expire 命令
    
    > Expire KEY_NAME TIME_IN_SECONDS
    > Redis Expire 命令用于设置 key 的过期时间。key 过期后将不再可用。
    > 设置成功返回 1
    > 当 key 不存在返回 0 