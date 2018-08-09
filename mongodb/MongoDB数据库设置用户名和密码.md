1.开发环境
+ Spring 4.2.5.RELEASE
+ Spring Data Mongodb 1.9.1.RELEASE
+ Mongo Java Driver 3.2.2
+ MongoDB 3.2  3.4

2.数据库操作
```shell
#进入用户管理数据库
use admin;
#创建超级管理员
db.createUser({user:'your_user_name',pwd:'your_user_password',roles:["root"]});
#使用超级管理员
db.auth("your_user_name","your_user_password");
#查看所有用户
db.system.users.find();
#删除用户 谨慎操作
#db.system.users.remove({user:"unxmongo"});
#进入一个数据库
use your_db;
#设置your_db的用户名和密码
db.createUser({user:'your_user_name',pwd:'your_user_password',roles:[{role:'readWrite',db:'your_db'}]});
#如果要修改用户的秘密,再次运行上面的语句或者使用下面的语句即可
db.createUser({user:'your_user_name',pwd:'your_new_user_password',roles:[{role:'readWrite',db:'your_db'}]});
#或者
db.changeUserPassword("your_user_name","your_new_user_password");
#其他创建数据库管理员
db.createUser({user:'your_user_name',pwd:'your_user_password',roles:[{role:"dbAdmin",db:'your_db'}]});
#创建所有用户的查看用户
db.auth("sysadmin","abc123");
db.createUser(
  {
    user: "unionx",
    pwd: "unionx!@#",
    roles: [ "readWriteAnyDatabase" ]
  }
);
```
3.开发环境设置 spring-mongo.xml文件配置
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mongo="http://www.springframework.org/schema/data/mongo"
       xsi:schemaLocation="http://www.springframework.org/schema/data/mongo http://www.springframework.org/schema/data/mongo/spring-mongo.xsd
    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.2.xsd">
    <mongo:repositories base-package="com.unionx"/>

    <mongo:mongo-client host="${mongo.host}" port="${mongo.port}" credentials="${mongo.user}:${mongo.password}@${mongo.dbname}" id="mongo">
        <mongo:client-options write-concern="SAFE"/>
    </mongo:mongo-client>

    <mongo:db-factory id="mongoDbFactory" dbname="${mongo.dbname}" mongo-ref="mongo"/>

    <bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
        <constructor-arg name="mongoDbFactory" ref="mongoDbFactory" />
    </bean>

    <bean class="org.springframework.data.mongodb.core.mapping.event.LoggingEventListener"/>
</beans>
```
4.数据库配置文件
```yaml
####################
# mongodb 连接配置 #
####################
mongo.host=101.200.168.176
mongo.port=27017
mongo.dbname=your_db_name
mongo.user=your_user_name
mongo.password=your_password
```
