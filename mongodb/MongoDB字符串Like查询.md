```shell
#假如需要查找的字符串为s,则可以用
db.tables.find({"name":/s/})
#或者
db.tables.find({"name":/^s/})
#或者
db.tables.find({"name":/s.*/})
#或者
db.tables.find({"name":/.s.*/})
```

###下面就分析下这几种查询的对应结果有什么不同：

#### 1.db.city.find({"extra_data.region":/.新.*/})

共765条记录：包含了【高新技术。高新区，虎丘。渝北区（含北部新区）】

【注：由结果可以看出所查字符前面必须有字符，相当于：db.city.find({"extra_data.region":/.新./})，也相当于db.city.find({"extra_data.region":/.新/})】

#### 2.db.city.find({"extra_data.region":/^新/})

共592条记录：包含了【新华。新洲。新都。新城。新区】

【注：由结果可以看出，此查询必须以所查字符开始】

#### 3. db.city.find({"extra_data.region":/新.*/})

共1357条记录：记录包含了【 新华。高新技术。渝北区（含北部新区）。高新区，虎丘】

【注：由结果可以看出前面字符可以有也可以没有，相当于：db.city.find({"extra_data.region":/新/})】

最后再分析下记录的结果，由上面三种查询可以看出，前两个查询的结果和正好等于最后一种的查询结果，这与注解完全符合。