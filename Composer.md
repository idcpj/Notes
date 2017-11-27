[TOC]

>参考网站[网址](https://www.greatcl.com/2016/09/02/create-your-first-composer-package/)
>Composer.json配置文件说明 [网址](http://blog.csdn.net/hel12he/article/details/46503875)

## 文件结构
```
0 talking_robot $ tree
.
└── src
    └── TalkingRobot
        └── Talk.php
└── test
└── doc
2 directories, 1 file
```

## `Talk.php`命名空间
```
namespace TalkingRobot;
class Talk
{
    public static function sayHello()
    {
        return 'Hello Composer';
    }
}
```

###  Composer 初始化项目
1.手动生成
2.`composer init`



## 技巧

### 安装未发布版本
如果自制包没有发布在composer.json中写
`"minimum-stability": "dev",`

安装时使用命令`composer require idcpj/talking_robot:dev-master`

