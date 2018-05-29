[TOC]

## 创建视图表
```sql
CREATE VIEW `tablename`AS select * from `wj_content`；
```


## 更新字段内容
```mysql
update `rb_carhome` SET `code_name`=replace(`code_name`,'NBRB0','NBRB') where code_name like 'NBRB0'
```

## HAVING 用法
用于配合group方法完成从分组的结果中筛选

`$this->field('username,max(score)')->group('user_id')->having('count(test_time)>3')->select(); `

## join用法
`INNER JOIN`: 等同于 JOIN（默认的JOIN类型）,如果表中有至少一个匹配，则返回行
`LEFT JOIN`: 即使右表中没有匹配，也从左表返回所有的行
`RIGHT JOIN`: 即使左表中没有匹配，也从右表返回所有的行
`FULL JOIN`: 只要其中一个表中存在匹配，就返回行

> `user.id=info.id`  当这个等式


## partition by  -  分组排序功能
[参考网址](https://www.cnblogs.com/zhwbqd/p/4205821.html)

如:获取所有用户最近的一笔消费
```sql
//通过对 money的create_time排序来获取最近一笔输出
select t.user_id, group_concat( t.money order by t.create_time desc ) moneys ... group by t.user_id
```