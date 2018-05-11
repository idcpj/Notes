[TOC]

## 简单demo
```
$sweet = array('a' => 'apple', 'b' => 'banana');
$fruits = array('sweet' => $sweet, 'sour' => 'lemon');

function test_print(&$item, $key)
{
    $item = "$key holds $item\n";
}

array_walk_recursive($fruits, 'test_print');
var_export($fruits);
/*
 [
     'sweet' => [
         'a' => 'a holds apple ',
         'b' => 'b holds banana ',
     ],
     'sour' => 'sour holds lemon ',
 ];
*/
```