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


##  更新操作
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


## 自动验证
model 模型中
```
protected $_validate  = array (
    array('name','2,6','申请人姓名不能为空',self::MUST_VALIDATE,'length'),
    array('phone','/^0?(13|14|15|17|18|19)[0-9]{9}$/','手机格式不正确',self::MUST_VALIDATE,'regex'),
    array('marital',array('未婚','已婚','离婚'),'婚姻内容不正确',self::VALUE_VALIDATE,'in'),
    array('other_userid','1,50','渠道方订单格式错误',self::VALUE_VALIDATE,'length'),
	array('other_userid','require','渠道方订单重复',self::VALUE_VALIDATE,'unique'),  //同一个字段可多次验证
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

## 打印某类日志
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

