[TOC]

>参考网站 [环境配置](http://www.devzhang.com/14526754330295.html)

## 环境配置
`sudo vim /etc/apache2/httpd.conf`

取消注释

`＃LoadModule php5_module libexec/apache2/libphp5.so`

添加 index.php

```
<IfModule dir_module>
     DirectoryIndex index.html index.php
</IfModule>
```

启动apache
`sudo apachectl start`

测试
地址中输入`localhost` 显示'it works'

## 修改站点位置

打开httpd.conf
`sudo vim /etc/apache2/httpd.conf`

修改默认路径
```
DocumentRoot "/Library/WebServer/Document"
<Directory “/Library/WebServer/Document”>
```
修改为
```
DocumentRoot "/Users/MyMacName/Web"
<Directory "/Users/MyMacName/Web">
```

测试配置是否正确
`apachectl configtest`

只要最后出现`syntax ok` 即说明配置正确

重启apache
`sudo apachectl restart`

## 多站点设置

取消注释
`#Include /private/etc/apache2/extra/httpd-vhosts.conf`

添加站点
` sudo vim /private/etc/apache2/extra/httpd-vhosts.conf`

站点实例
```
<VirtualHost *:80>
    DocumentRoot "/Users/idpcj/Web/demo"
    ServerName www.demo.com
    <Directory "/Users/idcpj/Web/demo">
    Options Indexes
    AllowOverride None
    Order deny,allow
    Allow from all
    </Directory>
 </VirtualHost>
```

编辑host
```
sudo vim /private/etc/hosts

127.0.0.1 www.demo.com
```

重启apache
`sudo apachectl restart`

## php.ini 优化

复制
`sudo cp /private/etc/php.ini.default /private/etc/php.ini`

编辑
`sudo vim /private/etc/php.ini
`

设置
```
date.timezone = PRC

display_errors = On

```
## brew 安装php
[参考网站](http://www.devzhang.com/14526754330295.html)
```
brew update
brew tap homebrew/php
brew install php55
```


## 安装 Mysql

安装
`brew install mysql`

设置开启启动
`ln -sfv /usr/local/opt/mysql/*.plist ~/Library/LaunchAgents`

启动
`mysql.server start`

设置密码
`mysql_secure_installation`

设置步骤
```
a)为root用户设置密码(可能有长度限制)

b)删除匿名账号

c)取消root用户远程登录

d)删除test库和对test库的访问权限

e)刷新授权表使修改生效
```