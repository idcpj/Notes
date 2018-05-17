[TOC]

## 创建http.php
在根目录下创建 `server/http.php`
```
$http = new swoole_http_server('0.0.0.0', 8811);
$http->set([
    'document_root'         => '/Users/idcpj/Web/swoole/thinkphp/public/static', //静态文件存放路径
    'enable_static_handler' => true,
]);
$http->on('WorkerStart', function (swoole_server $server){
    define('APP_PATH', __DIR__ . '/../application/');
    //// 加载基础文件
    require __DIR__ . '/../thinkphp/base.php';
});
//在 request 中执行代码
$http->on('request', function ($request, $response) use ($http){
    //把值赋值给$_SERVER,$_GET,$_POST 方便tp5快加执行
    $_SERVER=[];
    if (isset($request->server)) {
        foreach ($request->server as $k => $v) {
            $_SERVER[strtoupper($k)] = $v;
        }
    }
    if (isset($request->header)) {
        foreach ($request->header as $k => $v) {
            $_SERVER[strtoupper($k)] = $v;
        }
    }
    $_GET=[];
    if (isset($request->get)) {
        foreach ($request->get as $k => $v) {
            $_GET[$k] = $v;
        }
    }
    $_POST=[];
    if (isset($request->post)) {
        foreach ($request->post as $k => $v) {
            $_POST[$k] = $v;
        }
    }

    ob_start();//开启缓存
    try{
        think\App::run()->send();
    } catch (Exception $e){
        //todo
    }
    $res = ob_get_contents();//获取缓存的内容
    ob_end_clean();
    //发送给浏览器
    $response->end($res);
    //$http->close();

});
$http->start();
```
由于 tp 的问题,此代码只有第一次访问的路径会成功,之后改变路径,都指向第一次访问的路径,只是由于 `onWorkerStart`  已经提前加载了 tp 代码导致,所以需要对tp 框架做调整

在`thinkphp/thinkphp/library/think/Request.php`中是注释代码

1. 在`path` 方法中
```php
//if (is_null($this->path)) {
	$suffix   = Config::get('url_html_suffix');
    $pathinfo = $this->pathinfo();
//}
```
2.  在`pathinfo`方法中
```
//if (is_null($this->pathinfo)) {
	code
}
```
 此时访问连接可以正常找到对应的控制器和方法
 但是此时连接必须是`/?s=index/index/demo`形式