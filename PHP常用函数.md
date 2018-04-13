[TOC]


## 常用php 函数

### array_walk
1. 引用传值

```
$fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");

function test_print(&$item2, $key)
{
    $item2=$key. "-".$item2;   //key 不可赋新值
}
array_walk($fruits, 'test_print');
print_r($fruits);//	 ['d' => 'd-lemon', 'a' => 'a-orange', 'b' => 'b-banana', 'c' => 'c-apple',]

```

