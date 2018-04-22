[TOC]

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
 12 xdebug.remote_enable=on
 13 xdebug.remote_enable=1
 14 xdebug.remote_mode="req"
 15 xdebug.remote_log="/var/log/xdebug.log"
 16 xdebug.remote_port=9000
 17 xdebug.remote_handler="dbgp"
 18 xdebug.idekey="PhpStorm"
 
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

