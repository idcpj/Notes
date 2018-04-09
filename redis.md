
[TOC]

> [phpredis中文手册](http://www.cnblogs.com/ikodota/archive/2012/03/05/php_redis_cn.html)

## 安装
`choco install redis`

php 安装redis 模块
[参考网址](https://segmentfault.com/a/1190000011725819)

### 5.6 nts-版
[php_redis模块](https://windows.php.net/downloads/pecl/releases/redis/2.2.7/php_redis-2.2.7-5.6-nts-vc11-x86.zip)
[php_igbinary 模块](https://windows.php.net/downloads/pecl/releases/igbinary/2.0.1/php_igbinary-2.0.1-5.6-nts-vc11-x86.zip)

## 开启
```
//进入目录
cd C:\Program Files\Redis
//开启 没有报错则说明成功
redis-server.exe conf/redis.conf
```
## 命令中测试
打开新命令行窗口
```
//连接
redis-cli.exe -h 127.0.0.1 -p 6379

//赋值
set test "hello word"

//取值
get test
```

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
                  'third_key'=>'third_val'
                  );
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

