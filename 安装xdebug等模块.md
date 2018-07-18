[TOC]
> [pecl 官网](http://pecl.php.net/)

## 手动修改php-config的extension_dir路径
```
which php-config

vim /usr/bin/php-config  

# 修改路径
extension_dir='/usr/local/Cellar/php@7.1/7.1.16_1/lib/ext'

```

## xdebug
> [参考网址](https://blog.csdn.net/maxsky/article/details/79788447)

1. 直接安装

> [参考网址](https://blog.csdn.net/maxsky/article/details/79788447)

下载,对应php版本
在` /usr/local/lib/php/` 新建一个 `php71` 文件夹，放入 `xdebug.so` 

配置参数

`/usr/local/etc/php/x.x/conf.d`，
新建文件` ext-xdebug.ini`，内容如下：

[Xdebug]
```
zend_extension="/usr/local/lib/php/extensions/xdebug.so"
;自动跟踪，可关闭（关闭后提升性能）
xdebug.auto_trace=On
;性能分析，可关闭（关闭后提升性能）
xdebug.profiler_enable=On
xdebug.var_display_max_children=512
xdebug.var_display_max_data=2048
xdebug.var_display_max_depth=8

xdebug.remote_autostart=on
xdebug.remote_enable=on
xdebug.remote_enable=1
xdebug.remote_mode="req"
xdebug.remote_log="/var/log/xdebug.log"
xdebug.remote_port=9000
xdebug.remote_handler="dbgp"
xdebug.idekey="PhpStorm"
```
2. 编译安装
看参考网址

```
tar -xzf xdebug-2.6.0.tgz
cd xdebug-2.6.0
phpize
./configure

# 等待上方命令完成后开始编译

make -j2

# 稍等 10s 左右，在 modules 目录即可得到 xdebug.so 文件 
之后的步骤与直接安装相同
```

## redis

> [参考网址](https://blog.csdn.net/joeson7456/article/details/79834176)

```
wget http://pecl.php.net/get/redis-3.1.6.tgz
cd redis-3.1.6
phpize
./configure
make && make install
```
生成 redis.so
`extension=/usr/lib/php/extensions/no-debug-non-zts-20160303/redis.so`

也可以讲`cd redis-3.1.6/modules/redis.so`放入指定位置,并手动添加位置
如:
放入`/usr/local/Cellar/php@7.1/7.1.16_1/lib/ext/redis.so`中

