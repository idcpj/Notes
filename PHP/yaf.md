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

### nginx 的 Rewrite
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

## php 代码补全
1. 克隆 `https://github.com/xudianyang/yaf.auto.complete` 到本地
2. 在 phpstrom 中引入文件`设置->语言&框架->php->include path`

## 应用第三方库的命名
如:
```
application/library/ThirdParty/Sms.php
//类名
class ThirdParty_Sms{}
```
类名为library 下的目录_文件名
