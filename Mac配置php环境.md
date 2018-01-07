[TOC]

>参考网站 [环境配置](http://www.devzhang.com/14526754330295.html)
>参考二[brew 安装环境多php版本](http://www.phpfensi.com/php/20150414/9254.html)

## 安装软件
```
brew tap homebrew/apache
brew tap homebrew/php

brew install httpd24
brew install php55 --with-apache --with-gmp --with-imap --with-tidy --with-debug
brew install mysql
```




## 环境apache
`vim /usr/local/etc/apache2/2.4/httpd.conf`

```
LoadModule php5_module /usr/local/Cellar/php5x/5.5.xx/libexec/apache2/libphp5.so
<IfModule mod_php5.c>

    AddType application/x-httpd-php .php
    AddType application/x-httpd-php-source .phps

    <IfModule mod_dir.c>
        DirectoryIndex index.html index.php
    </IfModule>
</IfModule>

#更改端口
Listen 80

#添加 index.php
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
<VirtualHost _default_:80>
    DocumentRoot "/Users/idcpj/Web"
    ServerName  localhost
</VirtualHost>

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
`sudo cp /usr/local/etc/php/5.5/php.ini /usr/local/etc/php/5.5/php.ini.bank`

编辑
`sudo vim /usr/local/etc/php/5.5/php.ini
`

设置
```
date.timezone = PRC

display_errors = On

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