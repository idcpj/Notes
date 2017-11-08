[TOC]

## 技巧
>自带.htaccess  无效

修改为: `			RewriteRule ^(.*)$ index.php/$1 [QSA,PT,L]  -->  RewriteRule ^(.*)$ index.php?/$1 [QSA,PT,L]`

>入口文件绑定
```
define('BIND_MODULE','admin');	
define('BIND_CONTROLLER','Index');
define('BIND_ACTION','index');
```

>创建新的入口文件
```php
//把index.php 内如复制到api.php
//浏览器访问 http://www.xxx.com/api.php
define('BIND_MODULE','api');  // -->api.php 只能访问api模块
define('BIND_MODULE','api/index'); 
```

>控制器输出

return 可以代替echo 输出 推荐使用return 输出

>事务回滚函数
```php
try{
    $db=Db::name('test');
    $arr=[
        "INSERT`dp_test`(`username`,`password`,`inttes`)VALUE('cpjinsert','passwor','1123')",
        "update`dp_test`set`username`='cpjupdate34'WHERE`id`=1",
    ];
    $res=$db->batchQuery($arr);
}catch(\Exception$e){
    dump($e->getMessage());
}
```


## 安装
### git 安装
```
git clone --depth=1 https://github.com/top-think/think.git think_git
cd think_git
git clone --depth=1 https://github.com/top-think/framework.git thinkphp 
```
### composer 安装
```
composer create-project --prefer-dist topthink/think think_composer
```

## 配置
### 扩展配置
在`config/extra/email.php`,写入配置参数email会被当作建名.
```php
//例子:  创建db.php
config/extra/databases.php
    return array(
        //code
);
```
### 场景配置
在`config/extra/config.php` 或 `app`中 的`config.php`中
配置  `'app_status'             => 'office'`,
创建`config/extra/office.php`   和`config/extra/home.php`
调节`app_status`的值`office`或`home`的参数.选择不同配置.
在不同场景下 databases 的设置不同

### 模块配置
