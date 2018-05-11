[TOC]

## 异步读文件
```
//方法一
swoole_async_readfile(string $filename, mixed $callback);

//方法二
bool swoole_async_read(string $filename, mixed $callback, int $size = 8192, int $offset = 0);
```

## 异步写文件
最大写入为4M,最后一个参数如果加`FILE_APPEND` 则追加文字
```
$file_content ="test 要写入的内容".PHP_EOL;
swoole_async_writefile(__DIR__.'/test.log', $file_content, function($filename) {
    echo "wirte ok.{$filename}".PHP_EOL;
}, FILE_APPEND);
```

### 使用场景
可再 http_server中加入访问日志
```
$http->on('request',function ($request,$response){
    $conent = [
        'date:'=>date('Y-m-d H:i:s',time()),
        'get:'=>$request->get,
        'post:'=>$request->post,
        'header:'=>$request->header,
    ];
    swoole_async_writefile(__DIR__ . '/access.log', json_encode($conent,JSON_UNESCAPED_UNICODE), function (){},        FILE_APPEND);
    $response->end('<h1>HTTPserver</h1>');
});
```