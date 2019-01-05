[TOC]


---
> packagist [包管理网站](https://packagist.org/packages/)
> [composer官网]()
---



## 发布自己的Composer
>参考网站[网址](https://www.greatcl.com/2016/09/02/create-your-first-composer-package/)

### 安装未发布版本
如果自制包没有发布在composer.json中写
`"minimum-stability": "dev",`

安装时使用命令
`composer require idcpj/talking_robot:dev-master`

### 配置自动更新

>参考官方教程网址[网址](http://blog.csdn.net/xionggang1024/article/details/77162007)

### 其他
>Composer.json配置文件说明 [网址](http://blog.csdn.net/pugongyinglhl/article/details/59521275)


## 使用composer

### 安装
1. 全局安装
[各个版本的教程](https://pkg.phpcomposer.com/#how-to-install-composer)
centos
```
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

2. 使用镜像-[参考网站](https://pkg.phpcomposer.com/)
	1.在全局配置镜像(推荐)
	在命令行中输入:
	`composer config -g repo.packagist composer https://packagist.phpcomposer.com`
    
	2. 修改项目镜像
	在项目根目录
    `composer config repo.packagist composer https://packagist.phpcomposer.com`
    你也可以手动添加镜像地址到composer.json文件
        ```
        "repositories": {
            "packagist": {
                "type": "composer",
                "url": "https://packagist.phpcomposer.com"
            }
        }
        ```
3. 出现ssl 报错
参考此[网站](http://www.ituring.com.cn/article/261281)

## 安装composer 包
1. 包存在composer.json中
`php composer.phar install` 或` composer.phar install`
