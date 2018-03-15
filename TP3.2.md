[TOC]

## 自动验证
model 模型中
```
protected $_validate  = array (
    array('name','2,6','申请人姓名不能为空',self::MUST_VALIDATE,'length'),
    array('phone','/^0?(13|14|15|17|18|19)[0-9]{9}$/','手机格式不正确',self::MUST_VALIDATE,'regex'),
    array('marital',array('未婚','已婚','离婚'),'婚姻内容不正确',self::VALUE_VALIDATE,'in'),
    array('address','1,20','地址内容不正确',self::VALUE_VALIDATE,'length'),
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