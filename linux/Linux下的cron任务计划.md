#Linux下的cron任务计划

+ 编辑任务计划

```
#设定某个用户的cron服务，一般root用户在执行这个命令的时候需要此参数  
crontab -u
#列出某个用户cron服务的详细内容
crontab -l
#删除某个用户的cron服务
crontab -r
#编辑某个用户的cron服务
crontab -e 
```