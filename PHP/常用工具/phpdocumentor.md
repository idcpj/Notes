[TOC]

## 问题 
### 无法支持 php7 ,则安装 php5.6
可能会无法支持 php7

## 手动安装一个 php5.6
```
> wget -c http://cn2.php.net/distributions/php-5.6.21.tar.gz
> tar -zxvf php-5.6.21.tar.gz
> cd php-5.6.21/
> ./configure  --prefix=/usr/local/php5 --enable-fpm --with-mysql  --with-mysqli --with-zlib --with-curl --with-gd --with-jpeg-dir --with-png-dir --with-freetype-dir --with-openssl --enable-mbstring --enable-xml --enable-session --enable-ftp --enable-pdo
> make
> make install
```
### 在项目目录无法使用 phpdoc
在php bin 目录如 `/usr/local/php5/bin`  执行 phpdoc
eg:
```
./phpdoc run -d /vagrant_data/application/controllers/  -t /vagrant_data/doc_api/
```

## 安装
```
pear channel-discover pear.phpdoc.org
pear install phpdoc/phpDocumentor
```
查看 phpDocumentor 的安装路径
如:`/usr/local/php/bin`
如果发现 `phpdoc -h`  查不到
把 执行文件加入环境变量`export PATH=$PATH:/usr/local/php/bin`

## 参数说明
```
-t	输出的文档保存的位置
-d	设置扫描的目录
-f	设置扫描的文件

--template   生成模板的样式
```
demo:
`phpdoc -d ./src  -d ./app  -t ./docs/api`
> 把`./src/`和`./app` 下的目录输出到`./docs/api`






