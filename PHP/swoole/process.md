[TOC]

## demo
创建一个子进程
```
$procoess = new swoole_process(function (swoole_process $pro){

    echo  "not output to term";
    //开启http_server.php 的进程
    $pro->exec('/usr/local/bin/php', [__DIR__."/../server/http_server.php"]);

},true);//如果第二个参数为 true  输出不会输出到屏幕中
$pid = $procoess->start();

//子进程
echo $pid . PHP_EOL;


//回收结束运行的子进程。 如上面代码的 http_server.php
swoole_process::wait();
```

查看父进程 id
`ps | grep process.php`  
process.php  为代码所在的文件名

通过父进程 id 查看 进程树,需要` brew  install pstree`
`pstree -p 26387`

## 使用场景
获取多个 url 中的内容
```
echo "process-start-time ". date('Y-m-d H:i:s',time()).PHP_EOL;

//传统获取 url 中的内容
$url =[
    'http://baidu.com',
    'http://sina.com.cn',
    'http://qq com',
    'http://baidu.com?search=singa',
    'http://baidu.com?search=singwa2',
    'http://baidu.com?search=imooc',
];

/*
foreach ($url as $v){
    $content []=curlData($v);
}
*/

for ($i=0; $i <6 ; $i++) {
    //子进程
    $process = new swoole_process(function (swoole_process $worker) use($i,$url){
       $content =  curlData($url[$i]);
       //方法1 输出到管道中
       echo $content.PHP_EOL;
       //方法2 输出到管道中
       $worker->write($content);
    },true);
    $pid = $process->start();

    $works[$pid] = $process;
}

//获取管道中的内容
foreach ($works as $process){
    echo $process->read();
}

function curlData($url){
    sleep(1);//假设耗时一秒
    return $url.'success'.PHP_EOL;
}

echo "process-end-time ". date('Y-m-d H:i:s',time()).PHP_EOL;

//总耗时只有 1秒 而非 6s
```




