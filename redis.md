
[TOC]

> [phpredis中文手册](http://www.cnblogs.com/ikodota/archive/2012/03/05/php_redis_cn.html)

## demo
```
$redis = new Redis();
$redis->connect('127.0.0.1', 6379);
$redis->ping()  //输出PONG 为正常  ,错误会报 RedisException 异常

//字符串操作
$redis->set("tutorial-name", "Redis tutorial");
$redis->get("tutorial-name");
$redis->delete("tutorial-name");

//存入多个值
$array_mset=array('first_key'=>'first_val',
	                  'second_key'=>'second_val',
	                  'third_key'=>'third_val');
$redis->mset($array_mset); #用MSET一次储存多个值
print_r($redis->get('third_key')); // third_val


//List(列表) 操作
$redis->lpush("tutorial-list", "Redis",'Oracle');
$redis->lpush("tutorial-list", "Mongodb");
$redis->lpush("tutorial-list", "Mysql");
// 获取存储的数据并输出
$arList = $redis->lrange("tutorial-list",0,3);
print_r($arList);  //数组形式的值

//获取key值
$arList = $redis->keys("*");
print_r($arList);  // 数组形式  Array ( [0] => tutorial-list [1] => tutorial-name )
```

