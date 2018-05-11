[TOC]

## swoole_timer_tick
> [参考网址](https://wiki.swoole.com/wiki/page/412.html)

设置一个间隔时钟定时器，与after定时器不同的是tick定时器会持续触发，直到调用swoole_timer_clear清除。
`int swoole_timer_tick(int $ms, callable $callback, mixed $user_param);`

回调函数
`function callbackFunction(int $timer_id, mixed $params = null);`
- $timer_id 定时器的ID，可用于swoole_timer_clear清除此定时器
- $params 由swoole_timer_tick传入的第三个参数

使用范围
在每个 `onOpen,onMessage,onclose`等等 都可以调用,是个函数,并非对象中的方法
## swoole_timer_after