[TOC]

## 准备工作
由于 redis 需要编译`./configure --enable-async-redis`

1. 安装 hiredis
`brew install hiredis`
3. 下载swoole
[github]( https://github.com/swoole/swoole-src/releases)
2. 解压
3. 安装
```
phpize
./configure --enable-async-redis
make clean
make -j
sudo make install
```
问题:
`php-m`发现swoole消失或者是通过p`hp --ri swoole`没有显示`async redis client`
```bash
vi ~/.bash_profile
在最后一行添加 export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
source ~/.bash_profile
```

## 案例
```
$redisClient  =new swoole_redis();
$redisClient->connect('127.0.0.1', 6379, function (swoole_redis $redisClient,$result){
    echo "connect======".PHP_EOL;
    var_dump($result); //true

    //设置值
    $redisClient->set('now_time',time(),function(swoole_redis $redisClient,$result){
        echo "set value ========".PHP_EOL;
        var_dump($result);//ok
        $redisClient->close();

    });

    //取值
    $redisClient->get('now_time',function(swoole_redis $redisClient,$result){
        echo "get value========".PHP_EOL;
        var_dump($result); //1526094676   now_time 的时间戳
        $redisClient->close();
    });

    //取所有值
    $redisClient->keys("*",function(swoole_redis $redisClient,$result){
        /*array (
          0 => 'now_time',
          1 => 'name',
          2 => 's',
        )  */
        var_export($result);
        $redisClient->close();
    });

});

echo "start".PHP_EOL;
```