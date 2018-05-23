+ 修改数据库用户密码
```
alter user postgres with password 'your_password';
```
+ 创建数据库用户 db_user_name
```
create user db_user_name with password 'db_user_password';
```
+ 给数据库用户db_user_name your_db_name
```
# 创建数据库后
grant all privileges on database your_db_name to db_user_name;
# 授权所有表的操作
grant select,insert,update,delete on all tables in schema public to db_user_name;
```