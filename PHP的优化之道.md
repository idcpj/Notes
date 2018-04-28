[TOC]

1. 如果某个函数中的变量需要多次调用,可以静态化属性
```
function send_http_status($code) {
    static $_status = array(
            // Informational 1xx
            100 => 'Continue',
            101 => 'Switching Protocols',
            // Success 2xx
            200 => 'OK',
            201 => 'Created',
            202 => 'Accepted',
            203 => 'Non-Authoritative Information',
            ...
            ...
    );
}
```
2. 递增一个未预定义的局部变量要比递增一个预定义的局部变量慢9至10倍。
3. 使用php 缓存技术,
4. 检测字符串长度
```
if (strlen($foo) < 5) { echo "Foo is too short"; }

if (!isset($foo{5})) { echo "Foo is too short"; }  //更优
```
5. 如果在代码中存在大量耗时的函数，你可以考虑用C扩展的方式实现它们。
6. 使用匿名函数在对象中做数组循环操作
可使用函数有`array_map()`
```
$fun = function($value){
    return $value*2;
};
print_r(array_map($fun,[1,2,3,4,5]));
```