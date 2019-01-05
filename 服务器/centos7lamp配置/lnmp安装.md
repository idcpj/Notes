[TOC]
> [官网](https://lnmp.org/install.html)

## 下载
`wget -c http://soft.vpser.net/lnmp/lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && sudo ./install.sh lnmp`

## 安装
`sudo ./install.sh`

## 常用命令
```
lnmp {start|stop|reload|restart|kill|status}
lnmp {nginx|mysql|mariadb|php-fpm|pureftpd} {start|stop|reload|restart|kill|status}
lnmp vhost {add|list|del}
lnmp database {add|list|edit|del}
lnmp ftp {add|list|edit|del|show}
lnmp ssl add
lnmp {dnsssl|dns} {cx|ali|cf|dp|he|gd|aws}
 
 ```

## 安装其他程序
```
./pureftpd.sh  # 安装 ftp 服务
./addons.sh install memcached  # 安装 memcached
./addons.sh install redis   # 安装 redis
```

## 目录
```
Nginx 目录: /usr/local/nginx/
MySQL 目录 : /usr/local/mysql/
MySQL数据库所在目录：/usr/local/mysql/var/
MariaDB 目录 : /usr/local/mariadb/
MariaDB数据库所在目录：/usr/local/mariadb/var/
PHP目录 : /usr/local/php/
```