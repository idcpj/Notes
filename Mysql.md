[TOC]

## 是数据库可以远程登录
```

mysql>  GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
mysql>  flush privileges;

username : 为mysql 的用户
password: mysql的密码
```

## 创建视图表
```sql
CREATE VIEW `tablename`AS select * from `wj_content`；
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
1. 简单demo
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


2. 如:获取所有用户最近的一笔消费
```sql
//通过对 money的create_time排序来获取最近一笔输出
select t.user_id, group_concat( t.money order by t.create_time desc ) moneys ... group by t.user_id
```
## 对表中的字段进行替换
```
//对write_price表中所有phone的157 替换为168
update write_price set phone=replace(phone, 157, 168);
```

## 开启全局日志
```
mysql>  SHOW VARIABLES LIKE 'general%';  //查看是否开启
mysql>  set GLOBAL general_log='ON';   //开启
```
> 日志路径为  `SHOW VARIABLES LIKE 'general%'` 显示的目录


## 开启慢查询

1. 查看慢查询的状态和保存位置
```
mysql> show variables like 'slow_query%';
```

2. 查看 慢查询事件
```
mysql> show variables like 'long_query_time';
```

3. 设置慢查询

> 慢日志输出的内容有两个，第一执行时间过长（大于设置的long_query_time阈值）；第二未使用索引，或者未使用最优的索引。

    方法一:
    mysql> set global slow_query_log='ON';  //设置慢查询日志存放的位置

    mysql> set global slow_query_log_file='/usr/local/mysql/data/slow.log'; //查询超过1秒就记录

    mysql> set global long_query_time=1;

    方法二:
    `my.ini`
    
    slow_query_log = ON
    slow_query_log_file = /usr/local/mysql/data/slow.log
    long_query_time = 1
    
   	//================================//
	分析慢查询语句
    分析出使用频率最高的前50条慢sql：
    /usr/local/services/mysql/bin/mysqldumpslow -s c -t 50 VM_166_154-slow.log

    如只需分析处理速度最慢的10条sql：
    /usr/local/services/mysql/bin/mysqldumpslow -t 10 VM_166_154-slow.
    

4. 重启 mysqk

5. 测试
`select sleep(2);`


## 关闭查询缓存
添加`SQL_NO_CACHE`
`SELECT SQL_NO_CACHE * form table_name`

## cpu 占用过高
`show full processlist  查看慢查询` 
