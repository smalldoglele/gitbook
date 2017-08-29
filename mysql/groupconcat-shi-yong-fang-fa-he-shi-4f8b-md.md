如下有一个航班表**wl_flight**，有两个字段航班号**number**和班期**plan**,
请写出sql，查询出包含0,1,2班期的所有航班的航班号

| id  | number | plan    |
| --- | ------ | ------- |
| 1   | 931    | 0       |
| 2   | 931    | 1       |
| 3   | 931    | 2       |
| 4   | 821    | 2       |
| 5   | 821    | 0       |
| 6   | 720    | 1       |
| 7   | 931    | 1       |

#### 答案

```sql
select plan from wl_flight group by plan
having group_concat(distinct number order by number separator '-')='0-1-2'
```