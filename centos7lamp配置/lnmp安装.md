[TOC]
> [官网](https://lnmp.org/install.html)

## 下载
`wget -c http://soft.vpser.net/lnmp/lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && ./install.sh lnmp`

## 安装
`sudo ./install.sh`

## 常用命令
```
 lnmp {start|stop|reload|restart|kill|status}
 lnmp {httpd|mysql|mariadb|pureftpd} {start|stop|reload|restart|kill|status}
 lnmp vhost {add|list|del}  #添加网站
 lnmp database {add|list|edit|del}
 lnmp ftp{add|list|edit|del}
 
 ```

## 安装其他程序
```
./pureftpd.sh  # 安装 ftp 服务
./addons.sh install memcached  # 安装 memcached
./addons.sh install redis   # 安装 redis

```