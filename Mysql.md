[TOC]

## 视图表
```sql
CREATE VIEW `tablename`AS select * from `wj_content`；
```


## 更新字段内容
```mysql
update `rb_carhome` SET `code_name`=replace(`code_name`,'NBRB0','NBRB') where code_name like 'NBRB0'
```
