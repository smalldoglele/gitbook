#### 查询dbref中的值
```
db.tumourDetect.find({memberName:'0809test'}).forEach(function(row){
  var dp=row.detectProjects;
  for(var i in dp){
    var id=dp[i].$id;
    var p=db.detectProject.findOne({_id:id});
    print(JSON.stringify(p))
  }
});
```