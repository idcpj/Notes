[TOC]
 
 > [response官方教程](https://wiki.swoole.com/wiki/page/540.html)

## 设置 cookie
在浏览器中查看 cookie 的值
```php
$http = new swoole_http_server('0.0.0.0', 8811);
$http->on('request',function ($request,$response){
    $response->cookie('cookiename','value',time()+1800);
    $response->end('<h1>HTTPserver</h1>');
});
$http->start();
```

## 获取 get/post参数
```php
$http->on('request',function ($request,$response){
     //print_r($request->get);//返回 get 参数 以数组形式
     //print_r($request->get['name']);//返回 get 参数 以数组形式
     //print_r($request->post); //
    $response->end('<h1>HTTPserver</h1>'.json_encode($request->get));
});
```

## 发送文件到浏览器
```
$http->on('request',function ($request,$response){
    //发送文件需要添加 header 指定文件类型
    $response->header('Content-Type', 'application/php');
    $response->sendfile(__DIR__.'/tcp.php');
    
    $response->end('<h1>HTTPserver</h1>');
});
```

### 访问静态静态文件
```
$server->set([
    'document_root' => '/data/webroot/www.democ.om', //静态文件存放路径
    'enable_static_handler' => true,
]);

//在统计目录下创建 data/index.html

//浏览器访问
http://127.0.0.1/data/index.hthml
//即可访问
```