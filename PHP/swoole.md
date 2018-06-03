[TOC]

> [官网](https://www.swoole.com/)
## 使用方式
异步 mysql,毫秒定时器,异步 redis,进程协程内存,异步文件,消息队列,异步task任务

## 安装
### pecl 安装
`sudo pecl install swoole`
重启 apache

### 源码安装
```
unzip swoole-swoole-v2.1.1.zip 
cd swoole/ 
#生成 configure 文件
/usr/local/src/php7.2.4/bin/phpize 

# 如果报错 Cannot find autoconf. 使用命令 yum install autoconf 安装即可
./configure --with-php-config=/usr/local/src/php7.2.4/bin/php-config

make && make install 进行编译
#编译完成后 在 php.ini 的最后一行加上 extension=swoole.so

php -m |grep swoole 查找 swoole 是否安装成功
```
##  四种回调函数
> [详情](https://wiki.swoole.com/wiki/page/458.html)
1. 匿名函数
2. 类静态方法
3. 函数
4. 对象方法

## http_server
`swoole_http_server`  继承 `swoole_server`中的所有方法


## 技巧
1.  此命令用于连接到想对应的 ip, 端口  可以快速查看是否连接上
```
 > telnet 127.0.0.1 9501   
 ```
 2. 关掉相应的端口
```
> lsof -i:9501

> kill   pid
```

## phpstorm 支持 php

[参考网址](https://www.jianshu.com/p/4a43d23f38af)

`https://github.com/eaglewu/swoole-ide-helper`
把 git 项目下载到本地
在 phpstorm 左侧目录中的外部库中添加当 git 项目的路径


## 基于 swoole 的框架
1. swoft
2. easyswoole
3. fastd