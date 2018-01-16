[TOC]

## 1. 在httpd.conf中加载重写模块

    `LoadModule rewrite_module modules/mod_rewrite.so`

## 2. 改写重定向权限
```
    DocumentRoot  "D:\phpStudy\WWW"
    <Directory />
        Options +Indexes +FollowSymLinks +ExecCGI
        AllowOverride All
        Order allow,deny
        Allow from all
        Require all granted
    </Directory>
```
>把AllowOverride  None 改为All
    

## 3. 重定向和伪静态的实现方法

	.htaccess文件
```
    原理
    .htaccess(分布式配置文件)提供了针对每个目录改变配置的方法
    其中的指定作用于此目录及所以子目录

    性能问题
    访问时,会查找所有上级的目录中的.htaccess文件
    可以被Apache主配置文件代替
```

## 4. mod_rewrite
    `Apache的URL操作模块
    包含 RewriteBase   RewriteRule   RewriteCond   RewriteMap`

## 5. rewrite日志功能
	实践操作
```
设置LogLevel alert rewrite:trace8(1~8)  
生产模式不要大于trace2

可能版本不同而有所不同

    httpd.conf
    LogLevel error   --->error可替换为以下/ 实践环境最好在crite以上

emerg 紧急 - 系统无法使用。
alert 必须立即采取措施。
crit 致命情况。
error 错误情况。 
warn 警告情况。 
notice 一般重要情况。
info 普通信息。
debug 出错级别信息 

日志存放在apache/logs/error.log下
```

## 6. RewriteRule 
    语法
        RewrtieRule 模式匹配 替换的URL [flags]
            ---模式匹配   支持Perl格式的正则表达式 和rewrite的变量
            ---替换的URL  支持模式匹配的结果和rewrite变量
            ---$1 通配符匹配的值为$1  $2为第二个匹配的值
                (.*)\.htm    $1.htm     $1=(.*)的值

    **R** 
        RewiteRule ^/?(.*)\.html$ /src/$1.php [R=302]
            ---R=302/301   不填为默认302  临时重定向 ,不会被服务器记录
            加R 浏览器地址中的值变为重定向的,
            否则只是在内部重定向

   **C**
        RewriteRule ^(.*)\.htm$ /$1.html [C]
        RewriteRule ^(.*)\.html$ /$1.php
        说明:*.htm 先跳转到1.html 在跳转到1.php

        连接下一条规则:只有匹配了第一条才进入第二条规则,例如果直接输入x1.html 不匹配第一条规则,就不会执行第二条

    **L**
        RewriteRule ^(.*) first.php?req=$1 [L]
        RewriteRule ^(.*) second.php?req=$1 

        匹配了第一条后,不执行第二条规则

    **NE**
        不对URL中的特殊字符进行hexcode转码
        RwwriteRule  ^(.*)\.htm /index.html#$1 [R,NE]

        不佳NE时候,#会转移为%23  

    **NC**
        RewriteRule ^test/(.*)\.htm /src/$1.html  [NC]    
        浏览器中的地址不区分大小写

    **G**
        RewriteRule ^test/.*$ - [G]   
        访问 www.foo.com/test/1.html   显示失效

    **QSA**
        RewriteRule ^per/(.*)$ /per.php?url=$1 [R,QSA]      
        不加QSA /pre/index.php?userame=cpj  --> /per.php?url=index.php
        加QSA   /pre/index.php?userame=cpj  --> /per.php?url=index.php&username=cpj 

## 7. URL-path
        RewriteBase /test/
        RewriteRule ^(.*)\.htm$ $1.html 
        在访问地址前自动加上/test
        访问/test/foo.html


## 8. RewriteCond 
    该指令定义了一个规则的条件,即在RewriteRule指令之前有一个或多个RewriteCond指令

    **$1~$9**   
        数字为第几个匹配的值
        ```
            RewriteCond $1 "test"
            RewriteRule ^(.*)\.htm$ /$1.html 
        ```
            只有匹配为test.htm 时候才跳转到test.html

    `%{NAME_OF_VARIABLE}`
    
    服务器变量应用(即$_SERVER)
        ```
            RewriteCond %{HTTP_HOST} "www.demo.com"
            RewriteRule ^(.*)\.htm$  http://localhost/$1.html 
        ```
        
        若host名为www.demo.com 则跳转到凹localhsot

   **%1~9**
        RewriteCond条件找那个最后符合的条件中的分组

        RewriteCond %{HTTP_HOST} "127.0.0.(.*)"
        RewriteCond %1 "2"
        RewriteRule ^(.*)\.htm$  http://localhost/$1.html  [R]

        必须满足127.0.0.2时候才进行跳转到localhsot

    CondPattern 
            -d 是否是目录   -f是否是文件(文件存在并且可以访问)
            RewriteCond   C:/wamp/www -d 

        [flags]
            [NC]  大小写敏感      [OR]条件判断的或  如果不加默认是and
            RewriteCond   C:/wamp/www/index.php  -F  [OR]
            RewriteCond   C:/wamp/license.txt  -F 
            #RewriteRule ^(.*)\.htm$ $1.html

            两个条件有一个满足就自行重写操作
## 8. RewriteMap

        RewriteMap Mapname MapType:MapSource
        -MapName   : 命名给RewriteRule调用
        -mapType   : map文件类型  有txt rnd
        -MapSource   : map 文件路径

        放在网站目录的外面,放置用户访问到

        txt格式
            $(MapName : LookupKey | DefaultValue)

            在httpd.conf中配置
            RewriteMap pages txt:c:/wamp/map.txt
                -pages  为文件名

            在map.txt
                test1 pagetest1        ->为文件名
                test2 pagetest2

            在.htaccess
                RewriteEngine on
                RewriteRule ^(.*)\.shtml ${pages:$1}


        rnd
            随机映射  
            在httpd.cof
                RewriteMap dirs rnd:c:/wamp/rnd.txt

            rnd.txt
                URL1 S1|S2|S3
                URL2 W1|W2|W3

            在.htaccess
                RewriteEngine on
                RewriteRule ^/(.*)\.shtml /${$dirs:$1|root}/$1.php

            解释
                访问www.foo.com/URL2/x1.shtml   ->www.foo.com/S2/x1.shtml

## 9. 防盗链
不显示图片
```
    RewriteCond %{HTTP_REFERER} !^$
    RewriteCond %{HTTP_REFERER} !^http://www.demo.com/.*$ [NC]
    RewriteRule \.(gif|jpg|png)$ –[F,NC]
```
显示禁止的图片
    
```
        RewriteCond %{HTTP_REFERER} !^$
        RewriteCond %{HTTP_REFERER} !^http://www.demo.com/.*$ [NC]
        RewriteRule \.(gif|jpg|png)$  localhost/demo/2.jpg [R]
```
## 10. ip限制
在httpd中(重启)
`RewriteMap hosts-deny txt:D:/wamp/hosts.deny`

在hosts-deny中
   ` 192.163.3.68 deny`
在.htaccess
```
RewriteEngine on
RewriteCond %{hosts-deny:%{REMOVE_ADDR}|NOTFOUND}  deny [OR]
RewriteCond %{hosts-deny:%{HTTP_HOST}|NOTFOUND}  deny 
RewriteRule ^ - [F]
```
## 11. 限制迅雷
通过特征分析,限制迅雷访问
```
RewriteCond %{HTTP_USER_AGENT} 2.0.50727 [NC,OR]  --如果是迅雷在HTTP_USER_AGNET中就有2.0.50727 
RewrtieCond %{HTTP_USER_AGENT} ^BlackWido  ^BlackWido [NC,OR]
RewriteRule   .     /demo.txt
```