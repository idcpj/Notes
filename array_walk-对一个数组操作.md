[TOC]

 1. 传入值为引用数组
 2. 在回调函数中可对值进行引用,无法对键名进行引用

## 对数组修改键值  ,引用形式
```
 $fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");
$func_walk =function (&$v,$k,$pre){
    $v=$v.'-'.$pre['name'];
};
array_walk($fruits, $func_walk, ['name'=>'fruit']);
var_dump($fruits);

/*
[
    'd' => 'lemon-fruit',
    'a' => 'orange-fruit',
    'b' => 'banana-fruit',
    'c' => 'apple-fruit',
]*/
```
