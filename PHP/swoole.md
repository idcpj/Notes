[TOC]

> [官网](https://www.swoole.com/)
## 使用方式
异步 mysql,毫秒定时器,异步 redis,进程协程内存,异步文件,消息队列,异步task任务

## 安装
### pecl 安装
`pecl install swoole`

### 源码安装
```
unzip swoole-swoole-v2.1.1.zip 
cd swoole/ 
/usr/local/src/php7.2.4/bin/phpize 生成 configure 文件
# 如果报错 Cannot find autoconf. 使用命令 yum install autoconf 安装即可
./configure --with-php-config=/usr/local/src/php7.2.4/bin/php-config

make && make install 进行编译
编译完成后 在 php.ini 的最后一行加上 extension=swoole.so

php -m |grep swoole 查找 swoole 是否安装成功
```
