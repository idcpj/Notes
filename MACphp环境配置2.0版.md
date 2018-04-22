[TOC]

> [参考网站-知乎](https://zhuanlan.zhihu.com/p/24614926)
## Apache 的安装

 ### 移除mac自带的 apache 服务,
```
$ sudo apachectl stop
$ sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null
```
### 并安装apache
` brew install httpd24 --with-privileged-ports --with-http2`

### 修改apache 配置
```apache
# 替换为自己的站点
DocumentRoot "/Users/idcpj/Web" 
<Directory "/Users/idcpj/Web">

#在 <Directory> 代码块里面，我们还需要将 AllowOverride 改为下面的样子：
AllowOverride All

#载入重写模块
LoadModule rewrite_module libexec/mod_rewrite.so

# 修改用户和用户组
User idcpj
Group staff
```

## PHP 的安装
```
$ brew install php55 --with-httpd24
$ brew unlink php55
$ brew install php71 --with-httpd24
```
## Apache 和 PHP 的配置
```
LoadModule php5_module        /usr/local/Cellar/php55/5.5.38_11/libexec/apache2/libphp5.so
LoadModule php5_module        /usr/local/Cellar/php71/7.1.0_11/libexec/apache2/libphp7.so
```
将上面的路径修改为：
```
LoadModule php5_module        /usr/local/opt/php55/libexec/apache2/libphp5.so
LoadModule php7_module        /usr/local/opt/php71/libexec/apache2/libphp7.so
```
/usr/local/opt/php71 其实是由 brew 创建的 /usr/local/Cellar/php71 的一个软连接。
升级 PHP 的小版本号的时候，比如由 7.1.0_11 时，我们就不需要再修改 LoadModule 对应的值了。

```
#LoadModule php5_module        /usr/local/opt/php55/libexec/apache2/libphp5.so
LoadModule php7_module        /usr/local/opt/php71/libexec/apache2/libphp7.so
```
##配置 PHP 的主目录索引文件
```
<IfModule dir_module>
    DirectoryIndex index.html
</IfModule>
```
将其替换为下面的代码：
```
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

<FilesMatch \.php$>
    SetHandler application/x-httpd-php
</FilesMatch>
```
强制重启apache
`sudo apachectl -k restart`

## 手动切换apache php版本
```
#LoadModule php5_module        /usr/local/opt/php55/libexec/apache2/libphp5.so
LoadModule php7_module        /usr/local/opt/php71/libexec/apache2/libphp7.so
```
## 脚本切换php版本
在`/usr/local/bin`中添加`sphp` 文件写入 [github脚本](https://gist.github.com/w00fz/142b6b19750ea6979137b963df959d11)的内容
```
并赋予执行权限
chmod +x /usr/local/bin/sphp
```

切换后,apache 和命令行中的php版本都回变化

```bash
sphp 55 
# sphp 71  
```


