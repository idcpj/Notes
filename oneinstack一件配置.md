[TOC]


##  一键安装php开发环境 

[oneinstack](https://oneinstack.com/install/)
技巧 一键安装
```
~/oneinstack/install.sh --apache_option 1 --php_option 7 --db_option 1 --php_extensions imagick --dbrootpwd idcpj --redis --phpmyadmin --reboot
```
## 添加附加组件
`./addons.sh`
![组件](https://static.oneinstack.com/images/addons.png)

## 添加虚拟主机
`./vhost.sh`
![添加虚拟机](https://static.oneinstack.com/images/vhost.png)

## 删除虚拟主机
`./vhost.sh del`
![删除虚拟机](https://static.oneinstack.com/images/vhost_del.png)

## 管理FTP账号
`./pureftpd_vhost.sh`
![FTP](https://static.oneinstack.com/images/pureftpd.png)

##  备份数据库和网站
`./backup_setup.sh`
![备份](https://static.oneinstack.com/images/backup_setup.png)
```
./backup.sh # Start backup, You can add cron jobs

    # crontab -l # Examples 
     0 1 * * * cd ~/oneinstack;./backup.sh  > /dev/null 2>&1 &
```
## 管理服务
```
# MySQL
service mysqld {start|stop|restart|reload|status}

#PHP
service php-fpm {start|stop|restart|reload|status}

#Apache
service httpd {start|restart|stop}

#Redis
service redis-server {start|stop|status|restart|reload}

#Memcached:
service memcached {start|stop|status|restart|reload}
```

## Opcache的缓存问题
如果使用Opcache 缓存,代码上传后,需要间隔2~3分钟才能生效

1. 方法一,卸载Opcache
```
cd /root/oneinstack
./addons.sh
```
![选择](https://oneinstack.com/wp-content/uploads/2017/04/uninstallopcache_cn.png)

2. 方法二：刷新PHP缓存
访问http://公网IP/ocp.php
或者直接访问http://公网IP/ocp.php?RESET=1 