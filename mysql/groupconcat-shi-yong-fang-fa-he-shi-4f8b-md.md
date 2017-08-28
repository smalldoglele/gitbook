如下有一个航班表**wl_flight**，有两个字段航班号**number**和班期**plan_no**

| id  | number | plan_no |
| --- | ------ | ------- |
| 1   | 931    | 0       |
| 2   | 931    | 1       |
| 3   | 931    | 2       |
| 4   | 821    | 2       |
| 5   | 821    | 0       |
| 6   | 720    | 1       |
| 7   | 931    | 1       |

####答案

```sql
select number from wl_flight groupby number
having group_concat(distinct plan_no order by plan_no separator,'-')='0-1-2'
```