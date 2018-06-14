[TOC]

> 由于pear 版本不支持 php7 使用 github 的版本
> [https://github.com/longxinH/xhprof](https://github.com/longxinH/xhprof)

## 安装
1. 安装
```
git clone https://github.com/longxinH/xhprof.git ./xhprof
cd xhprof/extension/
/path/to/php7/bin/phpize
./configure --with-php-config=/path/to/php7/bin/php-config
make && sudo make install
```
2. 配置
```
[xhprof]
extension = xhprof.so
xhprof.output_dir = /tmp/xhprof
```
> 注意生成目录的权限问题

## demo
```

xhprof_enable();

/*==================start index.php 文件==================*/
define('APPLICATION_PATH', dirname(__FILE__));
$application = new Yaf_Application( APPLICATION_PATH . "/conf/application.ini");
$application->bootstrap()->run();
/*==================end==================*/

$xhprof_data = xhprof_disable();
print_r($xhprof_data);
include_once APPLICATION_PATH. "/application/library/ThirdParty/xhprof_lib/utils/xhprof_lib.php";
include_once APPLICATION_PATH. "/application/library/ThirdParty/xhprof_lib/utils/xhprof_runs.php";
// save raw data for this profiler run using default
// implementation of iXHProfRuns.
$xhprof_runs = new XHProfRuns_Default();
// save the run under a namespace "xhprof_foo"
$run_id = $xhprof_runs->save_run($xhprof_data, "xhprof_foo");

echo "---------------\n".
     "Assuming you have set up the http based UI for \n".
     "XHProf at some address, you can view run at \n".
     "http://<xhprof-ui-address>/index.php?run=$run_id&source=xhprof_foo\n".
     "---------------\n";
 ```
 
 ## 显示性能文件
 **需要把github 项目中的 `xhprof_html` 目录 和`xhprof_lib` 放到项目的根目录中**
 
 此时生成的`xhprof_foo` 文件 可以通过`xhprof_html`访问到

