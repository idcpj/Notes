[TOC]

## Swoole task任务使用
继承 server 的类都可以使用 task 任务
```
class ws{
    const HOST = '0.0.0.0';
    const PORT = 8812;

    public $ws = null;

    public function __construct(){
        $this->ws = new swoole_websocket_server(self::HOST, self::PORT);
        $this->ws->set([
            'work_num'=>2,
            'task_worker_num'=>2, //要使用 task  必须设置 task_worker_num 的值
        ]);
        $this->ws->on('open',[$this,'onOpen']);
        $this->ws->on('message',[$this,'onMsg']);
        $this->ws->on('task',[$this,'onTask']);
        $this->ws->on('finish',[$this,'onFinish']);


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
        $data=[
            'name'=>'cpj',
            'fd'=>$frame->fd
        ];
        $ws->task($data);
        $ws->push($frame->fd,'server-push'.date('Y-m-d H:i:s',time()));
    }

    //$task_id和$src_worker_id组合起来才是全局唯一的，不同的worker进程投递的任务ID可能会有相同
    public function onTask($ws,$task_id,$src_worker_id,$data){
        print_r($data);
        sleep(10);
        return "on task finish"; //告诉 worker
    }

    //接收到的 $data 就是 onTask return 内容
    public function onFinish($ws,$task_id,$data){
        echo "taskId : ".$task_id;
        echo "finish-data-success:{$data}";
    }

    public function onClose($ws,$fd){
        echo "clientid:{$fd}\n";
    }
}

$obj = new ws();
```
使用
1. 通过 http_server 或直接 web_socker 访问,当 js 触发`websocker.send("todo")`
2. 触发  message 事件,在 massage 中触发 task 事件
3. 触发 task 后触发 onTask 的回调
4. 回调完成后触发 onFinish  事件
