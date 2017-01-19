+ 常用操作命令

```bash
#创建数据库
use database_name
#显示数据库（非空）
show　dbs
#删除数据库（use之后）
db.dropDatabase()
#插入文档
db.collection_name.insert(document)
#也可以直接向数据库插入
db.database_name.insert(document)
#显示所有集合(表)show collections
#help命令的用法
help
db.help();
db.yourColl.help();
db.youColl.find().help();
rs.help();
```
+ 数据的导入导出

```bash
#将数据库test中集合user的数据以json的格式导出到user.json文件中
mongoexport -d test -c user -o d:/test/mongodb/user.json
#同上，导出为csv，【需要指定列，因为col列数是不固定的】
mongoexport -d test -c user --type=csv -f _id,name,age,home -o d:/test/mongodb/user.csv
#将user.json中的数据导入到数据库test的user中
mongoimport -d test -c user d:/test/mongodb/user.json
#将数据库copy到
db.copyDatabase(<from_dbname>, <to_dbname>, <from_hostname>, <username>,<password>);
```
+ 数据操作语言DML

```bash
####dml数据操纵语言#将数据插入到数据库
db.col.insert();
#将数据存入数据库,不指定_id和insert一样 指定了_id就是update
db.col.save();
#更新数据,multi参数重要，更新多条还是一条#update更新的操作符 $set
db.collection.update(<query>,<update>, {upsert: <boolean>,multi: <boolean>,     writeConcern: <document>})
#remove删除表
db.collection.remove(<query>, {justOne: <boolean>,writeConcern:<document>})
#删除所有数据()
db.col.remove({});
#查询文档格式化输出db.col.find().pretty()
#条件or
db.col.find({$or: [{key1: value1}, {key2:value2}]}).pretty()
#名字=walden1 年龄大于24
db.user.find({$or:[{name:'walden1'},{age:{$gt:24}}]});
#家乡是PY,(大于等于29岁，小于22岁的)
db.user.find({home:'PY',$or:[{age:{$gte:29}},{age:{$lt:22}}]});
#查询指定的列 find第二个参数，0表示不显示 1或者其他数字表示显示
db.user.find({},{name:1,_id:0});
#默认数字double 1 string 2 object 3 array 4
db.col.find({"title" : {$type : 2}})
#limit方法控制NUMBER条数
db.col.find().limit(NUMBER);
#返回2条数据db.user.find().limit(2);
#skip()方法来跳过指定数量的数据
db.user.find().skip(2).limit(2);
#sort()  1 升序 2 降序
db.user.find().sort({age:-1});
```
+ 索引

```bash
#索引或者聚合#索引是特殊的数据结构，索引存储在一个易于遍历读取的数据集合中，索引是对数据库表中一列或多列的值进行排序的一种结构#1表示升序索引 -1表示降序索引
db.user.ensureIndex({name:1});
#复合索引
db.user.ensureIndex({age:1,home:1});
#参数 background 后台执行 unique 是否唯一 name 索引名
db.values.ensureIndex({open: 1, close: 1}, {background: true})
```
+ MapReduce

```bash
db.collection.mapReduce(
    function() {emit(key,value);},//map 函数
    function(key,values) {return reduceFunction},//reduce 函数
    {
        out: collection,
        query: document,
        sort: document,
        limit: number
    }
);
####例子
> db.user.mapReduce(
    function(){emit(this.home,1);},
    function(key,value){return Array.sum(values)},
    {
        query:{age:{$gte:25}},
        out:'user_total'
    }
).find();
```
+ 表关联的使用分析

```bash
###############################
1-1
#尽量放一起
Face{noses:[]}
Nose
#如果设计上有明显的好处，硬要分开
Face:{nose_id:'1232'}
Nose:{face_id:'567'}
###############################
1-n
#例子PostComment
#当n小于100的时候
Post:{comments:[{},{},{},{}]}
#当n大于1000，小于10000的时候
Post:{comment_ids:[]}
#大于10000到正无穷Comment:{post_id:'ididididid'}
###############################
n-1
反过来同一对一
###############################
n-n(多对多，业务层面一般的多不会真多)
Student:{course_ids:[id,]}Course:{student_ids:[id,]}
###############################
#起步1W到正无穷如果数据量特别大，才考虑用关联表推荐文章：（高质量译文）http://blog.csdn.net/zythy/article/details/33725981
###############################
```
+ 更新操作符

```bash
$set
$unset 删除键值
$inc 数字类型的增加&减少
$push 数组类型插入一个值
$pushAll 数组类型 插入一个数组的所有元素
$pull 数组类型删除一个值
$pullAll 删除一个数组中的值
$addToSet 数组类i系那个插入一个值，如果这个值存在，不添加
$pop 删除一个元素 正数 尾部删除 负数 开头删除
$rename 修改字段名称
$bit 位操作 {$bit : { field : {and : 5}}}
```
+ spring data mong 配置片段

```xml
<?xml version="1.0" encoding="UTF-8"?><beans xmlns="http://www.springframework.org/schema/beans"       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"       xmlns:mongo="http://www.springframework.org/schema/data/mongo"       xsi:schemaLocation="http://www.springframework.org/schema/data/mongo http://www.springframework.org/schema/data/mongo/spring-mongo-1.0.xsd    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.2.xsd">
  <mongo:repositories base-package="com.unionx.ylbs.bbs.repository"/>
  <!-- Default bean name is 'mongo' -->
  <mongo:mongo host="localhost" port="27017"/>
  <mongo:db-factory dbname="test" mongo-ref="mongo" />
  <bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
    <constructor-arg name="mongoDbFactory" ref="mongoDbFactory"/>
</bean>
  <bean class="org.springframework.data.mongodb.core.mapping.event.LoggingEventListener"/>
</beans>
```
+ spring 中代码连接数据库

```java
new MongoTemplate(new MongoClient(), "database");
UserCredentials userCredentials = new UserCredentials("joe", "secret");
mongoDbFactory=new SimpleMongoDbFactory(new Mongo(), "database", userCredentials);
new MongoTemplate(mongoDbFactory());
```


