[TOC]

## 对多维数据进行排序
```
$data[] = array('volume' => 67, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 1);
$data[] = array('volume' => 85, 'edition' => 6);
$data[] = array('volume' => 98, 'edition' => 2);
$data[] = array('volume' => 86, 'edition' => 6);
$data[] = array('volume' => 67, 'edition' => 7);


array_map(function($item)use(&$tmp){
    $tmp['volume'][]=$item['volume'];
    $tmp['edition'][]=$item['edition'];
}, $data);

// 将数据根据 volume 降序排列，根据 edition 升序排列
// 把 $data 作为最后一个参数，以通用键排序
array_multisort($tmp['volume'], SORT_DESC, $tmp['edition'], SORT_ASC, $data);
var_dump($data);

//以volume 为第一个排序方式,edtion 为第二排序方式
/*[
 0 => ['volume' => 98, 'edition' => 2,],
 1 => ['volume' => 86, 'edition' => 1,],
 2 => ['volume' => 86, 'edition' => 6,],
 3 => ['volume' => 85, 'edition' => 6,],
 4 => ['volume' => 67, 'edition' => 2,],
 5 => ['volume' => 67, 'edition' => 7,],
];*/
```