[TOC]


## 常用php 函数
### array_walk
1. 引用传值

```php
$fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");

function test_print(&$item2, $key){
    $item2=$key. "-".$item2;   //key 不可赋新值
}
array_walk($fruits, 'test_print');
print_r($fruits);//	 ['d' => 'd-lemon', 'a' => 'a-orange', 'b' => 'b-banana', 'c' => 'c-apple',]

```
2. 传参赋值,可传字符串,数组
```php
$fruits = array("d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple");

function test_alter(&$item1, $key, $prefix){
    //$item1 = "{$prefix['name']}: $item1";
    $item1 = "{$prefix['name']}: $item1";
}

array_walk($fruits, 'test_alter', ['name'=>'cpj']);
print_r($fruits); //[ 'd' => 'cpj: lemon', 'a' => 'cpj: orange', 'b' => 'cpj: banana', 'c' => 'cpj: apple',]
```
### array_walk_recursive 
可引用  可赋值 
```
$sweet = array('a' => 'apple', 'b' => 'banana');
$fruits = array('sweet' => $sweet, 'sour' => 'lemon');

function test_print(&$item, $key,$prefix){
    $item = "new-".$prefix['name'].'-'.$key;
}

array_walk_recursive($fruits, 'test_print',['name'=>'cpj']);
var_export($fruits);

/*[ 'sweet' => [
    'a' => 'new-cpj-a',
            'b' => 'new-cpj-b',
        ],
    'sour' => 'new-cpj-sour',
]*/
```