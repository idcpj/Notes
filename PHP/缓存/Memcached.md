[TOC]

> [官网手册](http://php.net/manual/zh/memcache.add.php)  
## demo

>
```
$memcache = new Memcache;             //创建一个memcache对象
$memcache->connect('localhost', 11211) or die ("Could not connect"); //连接Memcached服务器

$memcache->set('key', 'key');        //设置一个变量到内存中，名称是key 值是test
$memcache->set('key1', 'key1');        //设置一个变量到内存中，名称是key 值是test

$memcache->get('key1');   //从内存中取出key的值
$memcache->delete('key1');  //刪除
$memcache->get('key1');  //bool值  false

$memcache->add('key10', 'value');
$memcache->add('key10', 'value1');
$memcache->get('key10');//value  add 不会进行覆盖

$memcache->set('name', array('cpj','age'=>17,'233'));
$memcache->get('name');   //可输出数组
```