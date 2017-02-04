+ 建表添加表和字段注释
```sql
create table t_user(
	id int(19) primary key auto_increment  comment '主键',
	name varchar(30) comment '姓名',
	create_time date comment '创建时间'
) comment  = '用户信息表';
```
+ 修改表/字段注释
```sql
alter table t_user comment  = '修改后的表注释信息(用户信息表)';
alter table t_user modify column id int comment '主键ID';
```
+ 查询数据库所有表的详细详细（含注释）
```sql
select * from information_schema.tables where table_schema='db_name' and table_name= 't_user';
```
+ 显示一个表的详细信息（字段注释，字段名称，类型）
```sql
select * from information_schema.columns where table_schema ='db_name'  and table_name = 't_user';
```
+ 另外比较简单的方式：
```sql
show full columns from table_name;
```