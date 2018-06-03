[TOC]

# ngnix 配置
```
server
    {
        listen 80;
        server_name www.yaf.com ;
        index  index.php ;
        root  /home/wwwroot/www.yaf.com;
        include enable-php-pathinfo.conf;
        access_log  /home/wwwlogs/www.yaf.com.log;
    }  
```
只需最精简即可