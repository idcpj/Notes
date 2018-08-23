[TOC]
>在循环时,我们需要查看每次循环的值,还不想等全部循环完,在输出值,可以用此方法

1. 每次都清空缓存
demo.php
```
header( 'Content-type: text/html; charset=utf-8' );
echo 'Begin ...<br />';
for( $i = 0 ; $i < 10 ; $i++ )
{
    echo $i . '<br />';
    ob_flush();
    flush();
    sleep(1);
}
echo 'End ...<br />';
```
2. 保存并输出缓存
```
ob_start();
echo "111111  ";
$res  =ob_get_clean();
echo "222222  ";
echo $res;
// 输出222222  111111
```


| code|作用|
|---|---|
|`ob_start()` |	开启ob缓存|
|`ob_get_contents()` |	获取ob缓存内容|
|`ob_clean()` |	清空ob缓存内容，不关闭ob缓存|
|`ob_end_clean()` |	清空ob缓存内容，并关闭ob缓存|
|`ob_flush()` |	将ob缓存的内容强制输出到程序缓存，不关闭ob缓存,不在ob_get_content中|
|`ob_end_flush()` |	将ob缓存的内容强制输出到程序缓存，并关闭ob缓存|
|`flush()` |	将数据强制输出至客户端 |