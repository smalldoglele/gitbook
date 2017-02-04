* 语法如下
```sql
select 
case when date is null then '合计'
     else date
end
as date,
sum(num) from `t` group by date 
with rollup;
```

* 效果如下图
  ![](/assets/sql_rollup.png)



