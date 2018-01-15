[TOC]

## 定时备份

如果 `php /data/www/demo/index.php  app sendApi cron`  无法备份,
可以使用访问地址的形式 `curl  http://www.demo.com/app/sendapi/cron`

使用命令备份时,需要注意的地方.
1. 文件权限是否限制
2. 如果php输出地方为相对路径,则保存的地方在 服务器 cd ~ 目录下,所以务必使用 绝对路径

>定时备份参看 [地址](https://www.kancloud.cn/martist/ma_zhao_liu/373726)

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
ini_set('memory_limit', '128M');
ignore_user_abort(true);
```
