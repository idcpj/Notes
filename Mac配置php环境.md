[TOC]

>参考网站 [环境配置(简书)](http://cdn2.jianshu.io/p/681397e16aec) ,  [Mysql安装(简书)](http://www.jianshu.com/p/3996f6a2fa45)

## 环境配置
`sudo vim /etc/apache2/httpd.conf`

注释

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