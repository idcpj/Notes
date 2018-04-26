[TOC]

## mysql 函数

###  group_concat
```sql
#以id 进行分组 ,把相同id 的name 用 , 隔开
select id,group_concat(name) as names from aa group by id;
+------+--------------------+
| id| names |
+------+--------------------+
|1 | 10,20,20|
|2 | 20 |
|3 | 200,500|
+------+--------------------+

```