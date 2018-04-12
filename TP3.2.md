[TOC]


## 配置设置
使用`C()`函数调用,可调用数组
1.配置目录为`模块名/Conf/config.php`
2.导入自定义的配置如`user.php等`
```
#在模块名/Conf/config.php中
return array(
		'LOAD_EXT_CONFIG' => 'user,email',
	);
#即可自动加载模块名下的user.php和email.php
```
## mysql的查询缓存 cache

```
//加key值可提高效率 也可通过 S('channel') 调用`
M("channel")->cache('channel',10)->select();
```
可通过在config.php 设置 `DATA_CACHE_TIME` 值来设置默认值.设置方法见[配置设置](#_2) ,原默认值为0,即永久缓存
```
return array(
	    'DATA_CACHE_TIME'=>60  //缓存时间为60秒
	);
```

## 用视图进行多表查询 ViewModel
```
在模块下的Model目录
class ChannelViewModel extends ViewModel{
    protected $viewFields=array(
        'Channel'=>array('id','channel_name','token','_type'=>'RIGHT'), //right对应下表的
        'Member'=>array('name','idcard','_on'=>'Channel.id=Member.channel_id')

    );
}

在控制器中调用
D("ChannelView")->where(array('id' => 47))->select() 以普通视图一样
```

## 数据库操作
###  更新操作
1. 方法一
```php

$channelData =D("Channel")->where(array('id'=>1));
//判断是否有值
if(!$channelData->find()){
	$this->error(暂无数据);
}
$channel->status=1;
$channel->save()
```
2. 方法二
```
$channel = D("Channel");
//直接在参数中写入主键,则视为更新
$data=array(
    'id'=>1,
    'create_time'=>111,
    'update_time'=>1112,
    'token'=>'',
);

if(!$channel->create($data)){
    $this->error($channel->getError());
}else{
    $channel->save();
}

```
###  查询操作
```php
//符合条件的一个值
D("test")->where(['age'=>11])->getField('id');  //return  String 2

//查询符合条件的多个值,第二个参数加true
D("test")->where(['age'=>11])->getField('id',true);  //return  array ( 0 => '2', 1 => '3')

//相同条件的记录条数操作和数据获得
$testDb = M("test")->where(['age'=>'11']);
$testClone =clone $testDb;
dump($testClone->count()); //取得条数
dump($testDb->select());    //取得数据

//通过条件查询字段
M('read_adv_media')->getFieldById($id,'aid');
```

### 自动验证
model 模型中
```
protected $_validate  = array (
	array('phone','require','手机号必填',1)
    array('name','2,6','申请人姓名不能为空',self::MUST_VALIDATE,'length'),
    array('phone','/^0?(13|14|15|17|18|19)[0-9]{9}$/','手机格式不正确',self::MUST_VALIDATE,'regex'),
    array('marital',array('未婚','已婚','离婚'),'婚姻内容不正确',self::VALUE_VALIDATE,'in'),
    array('other_userid','1,50','渠道方订单格式错误',self::VALUE_VALIDATE,'length'),
	array('other_userid','','渠道方订单重复',self::VALUE_VALIDATE,'unique'),  //同一个字段可多次验证
);

//验证后的操作
protected $_auto=array(
    array('create_time','time',self::MODEL_INSERT,'function'),
    array('update_time','time',self::MODEL_BOTH,'function'),
    array('our_orderid','sp_get_order_sn',self::MODEL_INSERT,'function'),
);
```
控制器中
```
$member = D("Member");
//注意有 ! 号
if (!$member->create($this->postData)){ //  如果为$_POST提交则不选在create中传入数据
    $this->error(303,$member->getError());
}
$member->add();
    
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

## 行为标签的使用方法
在`application/Common/Behavior`中添加行为
```
class DemoBehavior extends Behavior {

    // 行为扩展的执行入口必须是run
    public function run(&$content){
    	print_r("hello word");
    }
}
```
在`application/Common/Conf/tags.php`中添加标签
```
return array( // 添加下面一行定义即可
    'app_init' => array(
        'Common\Behavior\InitHookBehavior',
        'Common\Behavior\DemoBehavior',
    ),
)
```

## T() 函数获取模版地址
```
T([资源://][模块@][主题/][控制器/]操作,[视图分层])
T('Public/menu');  //当前模块

$this->display(T('Admin@Public/menu'));
```

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