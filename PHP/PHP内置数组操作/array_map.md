[TOC]

`array array_map ( callable $callback , array $array1 [, array $... ] )`
**主要针对多个数组操作,结果返回到第一个数组中**
**执行结果是以第一个传入的数组键名为基础的**


## 对一个数组进行操作
```php
$func = function($value) {
    return $value * 2;
};
print_r(array_map($func, range(1, 5));
```

## 传入外部变量
```
$double = 3;
$func = function($value) use($double){
    return $value .'-'. $double;
};
$a = ['name'=>'cpj','age'=>12];
$mapArr = array_map($func, $a); //array ( 'name' => 'cpj-3', 'age' => '12-3', )

```
## 使用自带函数
```
$c = array_map('trim', $a);
```