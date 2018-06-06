[TOC]

> [手册](http://www.laruence.com/manual/)
## 安装 yaf 扩展
通过`http://pecl.php.net/package/yaf` 官网安装

## 生成官方 demo
```
> https://github.com/laruence/yaf`
> cd tools/cg
> ./yaf_cg
> cd output
> tree  # 查看目录结构
```
## 配置伪静态化

### Apache的Rewrite
```
#.htaccess, 当然也可以写在httpd.conf
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule .* index.php
```

### 
```
server {
  listen ****;
  server_name  domain.com;
  root   document_root;
  index  index.php index.html index.htm;

  if (!-e $request_filename) {
    rewrite ^/(.*)  /index.php/$1 last;
  }
}
```
