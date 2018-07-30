# 判断一个字段是否存在
```
db.users.find({age:{$exists:true});
```
# 修改一个字段的名字
···
db.users.update({},{$rename:{"old_name","new_name"}},false,true);
···