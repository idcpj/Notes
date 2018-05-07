[TOC]


## 导入自定义的配置如
如`user.php等`
```
#在模块名/Conf/config.php中
return array(
		'LOAD_EXT_CONFIG' => 'user,email',
	);
#即可自动加载模块名下的user.php和email.php
```


## 指定打印某类日志
```
define("APP_DEBUG", false);  //必须关闭调试模式,不然,会有多余日志类型

封装好的日志类
function writelog($msg){
	C('LOG_PATH',SITE_PATH.'data/runtime/Logs/'.CONTROLLER_NAME.'/debug/');
	\Think\Log::record($msg,\Think\Log::DEBUG,true);
}
```

## 行为标签-Behavior
1. 在已有标签中添加行为 ,如`app_init`


3. 创建标签,并添加行为
创建在应用模块的`Home/Behavior/TestBehavior.class.php`
```
namespace Home\Behavior;
use Think\Behavior;

class TestBehavior extends Behavior{
    public function run(&$pram){
        $pram.="Word";
    }
}
```

在`Conf/tags.php`  注意 tag后有加s
```
return [
    'my_tag' => array(
        'Home\Behavior\TestBehavior',
    ),
];
```
在控制器中写入代码
```
$params = 'Hello';
Hook::listen('my_tag',$params);

print_r($params); //Hello Word
```
> 注:由于run方法不返回值,但是由于是引用传值,所在run中所做的修改在控制器中依然会变



## 在模版中插入 include
```
<include  file="admin/demo" /> #admin模块下的 demo,并不在某个控制器对应目录下
```
1. 传值方式一,在表中输入值
```
<include  file="admin/demo"  title="hellol word"/>
demo.html中

<p>[title]</p>
```
2. 如果是同一变量名,无需传值
```
<!--如果在住模版中有 $lists,则无需传值-->
<foreach name="lists" item="vo">
    <tr>
        <td>{$vo.id} </td>
        <td>{$vo.name}</td>
    </tr>
</foreach>

```

## RESTFul APi 接口
[参考文档](https://www.kancloud.cn/manual/thinkphp/1879)
>如果某控制器为纯接口形式,则也可继承该方法,而无需设置

在模块名/userController  控制器中 创建继承RestController的方法
```
class UserController extends RestController{
    protected $allowMethod    = array('get','post','put','delete'); // REST允许的请求类型列表
    protected $allowType      = array('html','xml','json'); // REST允许请求的资源类型列表

    Public function index(){
        switch($this->_method){
            case 'get':
            	//todo
                $this->response(array('name'=>'cpj','age'=>12),'json',200);
                break;
            case 'put':
            	//todo
                $this->response(array('name'=>'cpj','age'=>12),'json',200);
                break;
            case 'post':
            	//todo
                $this->response(array('msg'=>'提交成功'),'json',200);
                break;
            case 'delete':
            	//todo
                $this->response(array('msg'=>'删除成功'),'json',200);
                break;
        }
    }
}
```
在data/conf/route.php 中添加 路由映射
```
return array (
	'User/:id'=>array('User/index'),
);
```
访问 `delete` 形式方法 `http://www.mapi.com/user/2`  则提示删除成功


## 生成静态缓存
>[查考文档](https://www.kancloud.cn/manual/thinkphp/1839)

在模块或commom /Conf/config.php中配额,

```
return array(
	'HTML_CACHE_ON'     =>    true, // 开启静态缓存
	'HTML_CACHE_TIME'   =>    60,   // 全局静态缓存有效期（秒）
	'HTML_FILE_SUFFIX'  =>    '.html', // 设置静态缓存文件后缀
	'HTML_CACHE_RULES' => array(
		// 定义静态缓存规则
		'*'=>array('{:module}/{:controller}/{:action}/{$_SERVER.REQUEST_URI|md5}'),//生成的文件路径,只要注意同样一个页面生成的路径一样即可
	)
);
```
生成静态文件后,如果存在静态文件,则提前与调用操作方法
```
public function show(){
    echo "hello word";  //存在静态缓存,则hello word 不会输出
    //todo
    $this->display();
}
```

## 生成Lite 文件,提升网站性能 
1. 在入口文件 `index.php`
`define('BUILD_LITE_FILE',true);`

2. 替换框架入口文件
```
require './ThinkPHP/ThinkPHP.php';
// 改成
require 'Application/Runtime/lite.php';  //即在index.php  中引入lite 文件即可.
```

3. 通过 `index.php` 访问即可

## 使用 trace
```
'SHOW_PAGE_TRACE' =>true,  //开启

//输出trace
trace($_GET,'用户信息');

//显示
用户信息:Array ( [p_reload] => 1 [reload_time] => 1524811491619 [bookcate] => 1 )

```

## 表单令牌
> 防止表单的重复提交

在`模块名/Conf/tags.php`中
```
return array(
     // 添加下面一行定义即可
     'view_filter' => array('Behavior\TokenBuild'),
    // 如果是3.2.1以上版本 需要改成
    // 'view_filter' => array('Behavior\TokenBuildBehavior'),
);
```
添加配置参数
`'TOKEN_ON'      =>    true,  // 是否开启令牌验证 默认关闭`
验证
```
$User = D("User"); 
 // 生成模型类的验证
 if (!$User->create($_POST)){
 // 令牌验证错误
 }
 ```
 
 ## 设置数据库缓存
 在`config.php`中配置
 `DATA_CACHE_TIME和DATA_CACHE_TYPE`
 ```
 //不带标识符
M('User')->where('id=5')->cache(true)->find();

/带标识符
M('User')->cache('key',60)->find();
 ```