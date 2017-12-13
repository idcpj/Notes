[TOC]

## demo

```
$memcache = new Memcache;             //创建一个memcache对象
$memcache->connect('localhost', 11211) or die ("Could not connect"); //连接Memcached服务器
$memcache->set('key', 'key');        //设置一个变量到内存中，名称是key 值是test
$memcache->set('key1', 'key1');        //设置一个变量到内存中，名称是key 值是test
$memcache->set('key2', 'key2');        //设置一个变量到内存中，名称是key 值是test
echo $memcache->get('key1');   //从内存中取出key的值

$memcache->add('key10', 'value');
$memcache->add('key10', 'value1');
echo $memcache->get('key10');//value  add 不会进行覆盖
```