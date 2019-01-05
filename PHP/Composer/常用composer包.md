[TOC]
> [参考网站,已有人整理php包](https://github.com/JingwenTian/awesome-php)


## 网络
### PHP Curl Class
> [github](https://github.com/php-curl-class/php-curl-class)

`composer require curl/curl"`
```
//get
$curl = new Curl\Curl();
$curl->get('http://www.example.com/search', array(
    'q' => 'keyword',
));

//post
$curl = new Curl\Curl();
$curl->post('http://www.example.com/login/', array(
    'username' => 'myusername',
    'password' => 'mypassword',
));

//down 不能下载https 的文件
$curl = new Curl();
$curl->download('https://www.example.com/image.png', '/tmp/myimage.png');
echo $curl->responseHeaders['Content-Type'] . "\n"; // image/png
echo $curl->responseHeaders['CoNTeNT-TyPE'] . "\n"; // image/png

```



## 验证

### fzaninotto/faker -生成验证数据
`composer requrie fzaninotto/faker`

```
$factory = Factory::create();
echo $factory->name;
echo $factory->city;
echo $factory->email;
```

## 电子商务
### OmniPay - 一个多网关支付处理的框架

[omnipay-paypal](https://github.com/thephpleague/omnipay-paypal) - PayPal 支付
[omnipay-wechatpay](https://github.com/lokielse/omnipay-wechatpay) - 微信支付
[omnipay-unionpay](https://github.com/lokielse/omnipay-unionpay) - 银联支付
[omnipay-alipay](https://github.com/lokielse/omnipay-alipay) - 支付宝支付
[omnipay-pingpp](https://github.com/phoenixg/omnipay-pingpp) - ping++聚合支付


## 文件

### 文件上传
`composer requrie  verot/class.upload.php`
```
$handle = new upload($_FILES['image_field']);
if ($handle->uploaded) {
  $handle->file_new_name_body   = 'image_resized';
  $handle->image_resize         = true;
  $handle->image_x              = 100;
  $handle->image_ratio_y        = true;
  $handle->process('/home/user/files/');
  if ($handle->processed) {
    echo 'image resized';
    $handle->clean();
  } else {
    echo 'error : ' . $handle->error;
  }
}
```