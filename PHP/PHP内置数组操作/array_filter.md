[TOC]

## 简单过滤
```
$data = ['volume' => 67, 'edition' => 2];
$res = array_filter($data, function($v){
    return $v>2;
});

var_export($res); //['volume' => 67,]
```
