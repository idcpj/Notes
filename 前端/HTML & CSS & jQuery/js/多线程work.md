[TOC]
> [阮一峰参考网站](http://javascript.ruanyifeng.com/htmlapi/webworker.html#toc2)

**注意事项:**
1. 同源限制
分配给 Worker 线程运行的脚本文件，必须与主线程的脚本文件同源。
2. DOM 限制
Worker 线程所在的全局对象，与主线程不一样，无法读取主线程所在网页的 DOM 对象，也无法使用document、window、parent这些对象。但是，Worker 线程可以navigator对象和location对象。
3. 通信联系
Worker 线程和主线程不在同一个上下文环境，它们不能直接通信，必须通过消息完成。
4. 脚本限制
Worker 线程不能执行alert()方法和confirm()方法，但可以使用 XMLHttpRequest 对象发出 AJAX 请求。
5. 文件限制
Worker 线程无法读取本地文件，即不能打开本机的文件系统 `file://`，它所加载的脚本，必须来自网络。


# 简单demo
 `Public/Admin/js/work.js`内容
```
console.log("hello word"); 
```

`index.html` 内容
```js
//由于 Worker 不能读取本地文件，所以这个脚本必须来自网络
var worker =new Worker('/Public/Admin/js/work.js');
```
控制台即可输出`hello word`

## 主进程与子进程交互demo
`index.html`内容
```
var worker =new Worker('http://192.168.0.70:8000/Public/Admin/js/work.js');

//1.主进程推送给子进程 可以使对象或者字符串等
worker.postMessage({method: 'echo', args: ['Work']});

//4.接受子进程过来的数据
worker.onmessage = function (event) {
    //可以在此处使用jquery
    $("body").css('background-color','red');
    console.log('Received message ' + event.data);
}
```

`work.js`内容
```
//2.把数处理后的程序发送给主进程
self.addEventListener('message', function (e) {
    //3.子进程处理传入的参数
    self.postMessage('You said: ' + e.data); //e.data 就是传入的数据
}, false);
```

## work 进程识别主进程的不同处理
```
self.addEventListener('message', function (e) {
  var data = e.data;
  switch (data.cmd) {
    case 'start':
      self.postMessage('WORKER STARTED: ' + data.msg);
      break;
    case 'stop':
      self.postMessage('WORKER STOPPED: ' + data.msg);
      self.close(); // Terminates the worker.
      break;
    default:
      self.postMessage('Unknown command: ' + data.msg);
  };
}, false);
```
