[TOC]

swool 提供了7个 内存操作模块
- Memory下的模块可以安全的用于异步非阻塞程序中，不存在任何IO消耗
- 所有模块均为多进程安全的，无需担心数据同步问题
- Memory相关模块对象为有限资源，不可大量创建

## Lock

## Buffe

## Table  -相当于创建 sql 表
```
//创建内存表
$table = new swoole_table(1024);

//内穿表增加一列
//swoole_table::TYPE_INT默认为4个字节，可以设置1，2，4，8一共4种长度
//swoole_table::TYPE_STRING设置后，设置的字符串不能超过此长度
//swoole_table::TYPE_FLOAT会占用8个字节的内存
$table->column('id', swoole_table::TYPE_INT,8);
$table->column('name', swoole_table::TYPE_STRING,13);
$table->column('age', swoole_table::TYPE_INT,9);
//创建
$table->create();


//创建一条数据,并且该数据的 key 为 table_key
$table->set('table_key', ['id'=>1,'name'=>'cpj','age'=>23]);

//第二种赋值方式
//$table['table_key'] = ['id'=>1111111,'name'=>'cpj','age'=>23];

//id 增加2 为3
$table->incr('table_key', 'id',2);


//获取数据
var_dump($table->get('table_key'));
//第二种取值方式
//var_export($table['table_key']->value);

//删值
$table->del('table_key');

var_dump($table->exist('table_key')); //return boolean
```


## Buffer

## table

## Atomic 

## mmap

## Channel

## Serialize