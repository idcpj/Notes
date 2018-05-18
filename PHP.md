[TOC]




## https双向认证
查看我的[github](https://github.com/idcpj/phplib/blob/master/src/Phplib/Curl.php)

## 证书转换
**PEM to DER**
`openssl x509 -outform der -in certificate.pem -out certificate.der`
**PEM to P7B**
`openssl crl2pkcs7 -nocrl -certfile certificate.cer -out certificate.p7b -certfile CACert.cer`
**PEM to PFX**
`openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt`
**DER(DER) to PEM**
`openssl x509 -inform der -in certificate.cer -out certificate.pem`
**P7B to PEM**
`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`
**PFX to PEM**
`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

>PXF转PEM后certificate.cer文件包含认证证书和私钥，需要把它们分开存储才能使用。


## 非静态方法转静态
```
//在方法中加入 new static()
public static function queryOneTrans($paramData){
    $beiyi = new static();

    $Debit = array();
    $Debit['merchantID'] = $beiyi->_merchantID; //商户id
    $beiyi->outlog("返回值",$fetchPost);
    $beiyi->_result($fetchPost);

}

//demo
BeiyiYanZheng::queryOneTrans($paramData);
```

## 重要操作避免程序操作超时或断开
```
ini_set("max_execution_time", 0);
set_time_limit(0);
ignore_user_abort(true);
ini_set('memory_limit', '128M');
```

## 商城框架
[Opencart](http://www.opencartchina.com/)
[prestashop](http://doc.prestashop.com/display/PS17/Getting+started+with+theme+development)


## ping++ 网页支付技巧
把[\Pingpp\Charge::create()](https://github.com/PingPlusPlus/pingpp-php/blob/master/example/recharge/recharge.php) 方法生成的json对象[pingpp.createPayment](https://www.pingxx.com/docs/client/web)
```js

//\Pingpp\Charge::create()返回的json变为js对象
var object={
    "id": "ch_LO0800TKunLGCy9ufHHmLmPS",
    "object": "charge",
    ...
}
pingpp.createPayment(object, function(result, err){
	 // 可按需使用 alert 方法弹出 log
    console.log(result);
    console.log(err.msg);
    console.log(err.extra);
    if (result == "success") {
    	// 只有微信公众号 (wx_pub)、QQ 公众号 (qpay_pub)支付成功的结果会在这里返回，其他的支付结果都会跳转到 extra 中对应的 URL
    } else if (result == "fail") {
        // Ping++ 对象不正确或者微信公众号 / QQ公众号支付失败时会在此处返回
    } else if (result == "cancel") {
        // 微信公众号支付取消支付
    }
});
```
## 回调函数的4种使用方式

```php
// 方法一: 直接传入函数名
array_map('my_callback_function',$arr); 

// 方法二: 用数组[类名,类方法]
array_map(array('MyClass', 'myCallbackMethod'),$arr); 

//方法三 : 传入实例化对象,加对象中的方法
$obj = new MyClass();
array_map(array($obj, 'myCallbackMethod'),$arr);
array_map([$this,myCallbackMethod],$arr);

//方法四 : 闯入静态方法
array_map('MyClass::myCallbackMethod');

//方法五 : 传入闭包函数
$double = function($a) {
    return $a * 2;
};
$new_numbers = array_map($double, $numbers);
