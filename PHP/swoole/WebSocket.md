[TOC]

## Web Socket 
Web Socket协议是基于TCP的一种新的网络协议。它实现了浏览器与服务器全双工full -duplex)通信——**允许服务器主动发送信息给客户端**。

http 的通信只能由客户端去发起

Websockett特点
- 建立在TCP协议之上
- 性能开销小通信高效
- 客户端可以与任意服务器通信
- 协议标识符 WS WSS
- 持久化网络通信协议

## demo
`server/websocket.php`

```
$server = new swoole_websocket_server("0.0.0.0", 8812);

$server->on('open', function (swoole_websocket_server $server, $request) {
    echo "server: handshake success with fd: {$request->fd}\n";
});
$server->on('message', function (swoole_websocket_server $server, $frame) {
    echo "receive from {$frame->fd}:{$frame->data},opcode:{$frame->opcode},fin:{$frame->finish}\n";
    //push 把数据发送给终端
    $server->push($frame->fd, "this is server");
});
$server->on('close', function ($ser, $fd) {
    echo "client {$fd} closed\n";
});
$server->start();
```

`data/ws_client.html`
```
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <title>Title</title>
</head>
<body>
<h1>测试</h1>
<script>
    var wxUrl = "ws://127.0.0.1:8812";
    var websocket = new WebSocket(wxUrl);
    //连接后触发
    websocket.onopen = function (event) {
        websocket.send("hello word"); //发送数据给websocket.php
        console.log("connnect-success");
    }
    websocket.onmessage = function (event){
        console.log('ws-server-return-data'+event.data);
    }
    websocket.onclose = function(event){
        console.log('close');
    }
    websocket.onerror = function(event){
        console.log('error:' + event.data);
    }
</script>
</body>
</html>
```

### 启动方法
在开启 webscoket.php状态下

1. 直接双击打开` ws_client.html` 
2. 通过 http_server.php 
然后在 http_server.php中设置了`document_root`的目录下打开
3. 只在websocket.php 中设置
```
$server->set([
    'document_root' => '/Users/idcpj/Web/swoole/data/', //静态文件存放路径
    'enable_static_handler' => true,
]);
```
然后直接访问静态文件即可,无需 http_server.php

## 面向对象的 demo
```
 class ws{
    const HOST = '0.0.0.0';
    const PORT = 8812;

    public $ws = null;

    public function __construct(){
        $this->ws = new swoole_websocket_server("0.0.0.0", 8812);
        $this->ws->on('open',[$this,'onOpen']);
        $this->ws->on('message',[$this,'onMsg']);
        $this->ws->on('close',[$this,'onClose']);

        $this->ws->start();
    }

    //监听连接事件
    public function onOpen($ws, $request){
        print_r($request->fd);
    }

    //监听ws消息事件
    public function onMsg($ws,$frame){
        echo "ser-push-message".$frame->data."\n";
        $ws->push($frame->fd,'server-push'.date('Y-m-d H:i:s',time()));
    }

    public function onClose($ws,$fd){
        echo "clientid:{$fd}\n";
    }
}
```