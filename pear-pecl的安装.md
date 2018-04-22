[TOC]

## 设置安装路径和引入路径
### php-config中设置安装路径

```
which php-config

vim /usr/bin/php-config  

# 修改路径
extension_dir='/usr/local/lib/php/pecl/20160303'
```
### 引入路径
在php.ini中
```
extension_dir = "/usr/local/lib/php/pecl/20160303"
```

## PEAR

> [pear 官方包列表](https://pear.php.net/packages.php)

### 安装
```
#这是一个安装 pear 的 php 发行包文件
wget http://pear.php.net/go-pear.phar
#执行安装
php go-pear.phar
```
### 升级到最新版本
```
pear upgrade --force PEAR
#更新下仓库
pecl channel-update pecl.php.net
```
### pear 安装扩展工具
```
pear install DB

downloading DB-1.9.2.tgz ...
Starting to download DB-1.9.2.tgz (133,795 bytes)
.............................done: 133,795 bytes
install ok: channel://pear.php.net/DB-1.9.2
```



## PECL
> [PECL 官网包列表](https://my.oschina.net/sallency/blog/693150)

### 安装
安装完`pear `后已有pecl
但是需要安装 一些组件
`brew install make cmake automake autoconf` 报错后安装

## 安装组件
```
pecl info redis

pecl install redis
pecl unisntall redis

pecl list 查看安装的列表
```