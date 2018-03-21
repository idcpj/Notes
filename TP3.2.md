[TOC]

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
	C('LOG_PATH',SITE_PATH.'data/runtime/Logs/debug');
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