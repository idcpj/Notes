[TOC]
>在循环时,我们需要查看每次循环的值,还不想等全部循环完,在输出值,可以用此方法

demo.php
```
header( 'Content-type: text/html; charset=utf-8' );
echo 'Begin ...<br />';
for( $i = 0 ; $i < 10 ; $i++ )
{
    echo $i . '<br />';
    flush();
    ob_flush();
    sleep(1);
}
echo 'End ...<br />';
```


| code|作用|
|---|---|
|`ob_start()` |	开启ob缓存|
|`ob_get_contents()` |	获取ob缓存内容|
|`ob_clean()` |	清空ob缓存内容，不关闭ob缓存|
|`ob_end_clean()` |	清空ob缓存内容，并关闭ob缓存|
|`ob_flush()` |	将ob缓存的内容强制输出到程序缓存，不关闭ob缓存,不在ob_get_content中|
|`ob_end_flush()` |	将ob缓存的内容强制输出到程序缓存，并关闭ob缓存|
|`flush()` |	强制把程序缓存的内容输出到浏览器缓存里面 ob_flush()后使用flush(),可以把内容输出到浏览器|