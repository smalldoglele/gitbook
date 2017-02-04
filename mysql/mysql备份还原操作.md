##**导出数据库**


1. 导出整个数据库
```
##mysqldump -u 用户名 -p 数据库名 > 导出的文件名  
mysqldump -u dbuser -p dbname > dbname.sql  
```
2.导出一个表
```
mysqldump -u 用户名 -p 数据库名 表名> 导出的文件名
mysqldump -u dbuser -p dbname users> dbname_users.sql
```
3. 导出一个数据库结构
```
mysqldump -u dbuser -p -d --add-drop-table dbname >d:/dbname_db.sql
```
> + -d 没有数据（也可以使用-no-data）
> + --add-drop-table 在每个create语句之前增加一个
> + DROP-TABLE IF EXISTS语句

4. 导出某个表的部分数据
```
mysqldump -u用户名 -p密码 数据库名 表名 --where="筛选条件" > 导出文件路径
```
######举例如下
```
#从test数据库的test_data表中导出id大于100的数据到 /tmp/test.sql 这个文件中
mysqldump -uroot -p123456 test test_data --where=" id > 100" > /tmp/test.sql
```
5. 导出数据库中的存储过程和函数
```
mysqldump -u [数据库用户名] -p -R [数据库用户名]>[备份文件的保存路径] 
```
6. 导出一个远程数据库到本地
```
mysqldump -h192.168.0.1 -u dbuser -p dbname > dbname.sql
```
> + h 远程数据库地址
> + 如果上述操作过程中遇到报错：
> + mysqldump:Couldn't execute ‘SELECT @@GTID_MODE':Unknown system variable 'GTID_MODE' (1193)
> + 造成此错误的原因是因为5.6引入了Global Transaction Identifiers (GTIDs) 。GTIDs可以让主从结构复制的跟踪和比较变得简单。
> + mysqldump会试图查询这个系统变量，但这个变量在5.6之前的版本中不存在，所以产生错误。
> + 的方法很简单。在mysqldump后加上–set-gtid-purged=OFF命令。如：
> + mysqldump -h dbHost -u dbuser dbName --set-gtid-purged=OFF >d:/db.sql
> + 注：这条命令最后不能加“;”分号，否则会报错：mysqldump: Couldn't find table ";"

7. 其他参数
```
–opt：此Mysqldump命令参数是可选的，如果带上这个选项代表激活了Mysqldump命令的quick，add-drop-table，add-locks，extended-insert，lock-tables参数，也就是通过–opt参数在使用Mysqldump导出Mysql数据库信息时不需要再附加上述这些参数。
–quick：代表忽略缓冲输出，Mysqldump命令直接将数据导出到指定的SQL文件。
–add-drop-table：顾名思义，就是在每个CREATE TABEL命令之前增加DROP-TABLE IF EXISTS语句，防止数据表重名。
–add-locks：表示在INSERT数据之前和之后锁定和解锁具体的数据表，你可以打开Mysqldump导出的SQL文件，在INSERT之前会出现LOCK TABLES和UNLOCK TABLES语句。表示在INSERT数据之前和之后锁定和解锁具体的数据表，你可以打开Mysqldump导出的SQL文件，在INSERT之前会出现LOCK TABLES和UNLOCK TABLES语句。
–extended-insert (-e)：此参数表示可以多行插入
--no-create-info(-t): 只导出数据，而不添加 CREATE TABLE 语句。
--no-data(-d): 不导出任何数据，只导出数据库表结构。
--default-character-set=charset：指定导出数据时采用何种字符集，如果数据表不是采用默认的 latin1 字符集的话，那么导出时必须指定该选项，否则再次导入数据后将产生乱码问题。
--hex-blob ：使用十六进制格式导出二进制字符串字段。如果有二进制数据就必须使用本选项。影响到的字段类型有 BINARY、VARBINARY、BLOB。
--where(-w): 来设定数据导出的条件。
```
##**导入数据库**'

1.source命令：
> + 进入mysql数据库控制台  
> + mysql>use 数据库  
> + 然后使用source命令，后面参数为脚本文件(如这里用到的.sql)  
> + mysql>source d:/dbname.sql

2.mysql 客户端还原
> mysql -uroot -p {databasename} <D:\m.txt