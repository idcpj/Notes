[TOC]

## 定时备份
如果 `php /data/www/demo/index.php  app sendApi cron`  无法备份,
可以使用访问地址的形式 `curl  http://www.demo.com/app/sendapi/cron`


## https双向认证

```php
function curl_post_ssl($url,$data){
			$tuCurl = curl_init();
			curl_setopt($tuCurl, CURLOPT_URL, $url);
			//curl_setopt($tuCurl, CURLOPT_PORT , 443);
			curl_setopt($tuCurl, CURLOPT_VERBOSE, 0);
			curl_setopt($tuCurl, CURLOPT_HEADER, 0);
			curl_setopt($tuCurl, CURLOPT_SSLVERSION, 1);

			curl_setopt($tuCurl,CURLOPT_SSLCERT,$this->_certUrl);  //-----BEGIN CERTIFICATE-----
			curl_setopt($tuCurl, CURLOPT_SSLCERTTYPE,"PEM");    //
			//curl_setopt($tuCurl,CURLOPT_SSLCERTPASSWD,$this->_keyPwd);      //证书密码

			curl_setopt($tuCurl,CURLOPT_SSLKEY,$this->_priKey);       // -----BEGIN RSA PRIVATE KEY-----
			curl_setopt($tuCurl, CURLOPT_SSLKEYPASSWD,$this->_keyPwd);
			curl_setopt($tuCurl, CURLOPT_SSLKEYTYPE,"PEM");

			//curl_setopt($tuCurl, CURLOPT_CAINFO,$this->_certUrl);//-----BEGIN PUBLIC KEY-----

			curl_setopt($tuCurl, CURLOPT_POST, 1);
			curl_setopt($tuCurl, CURLOPT_RETURNTRANSFER, 1);//是否返回数据流
			curl_setopt($tuCurl, CURLOPT_SSL_VERIFYPEER, 0);

			curl_setopt($tuCurl, CURLOPT_POSTFIELDS, $data);
			//curl_setopt($tuCurl, CURLOPT_HTTPHEADER, array("Content-Type: text/xml","SOAPAction: \"/soap/action/query\"", "Content-length: ".strlen($data)));

			$tuData = curl_exec($tuCurl);
			if(!curl_errno($tuCurl)){
				//$info = curl_getinfo($tuCurl);
				//echo 'Took ' . $info['total_time'] . ' seconds to send a request to ' . $info['url'];
			} else {
				echo 'Curl 错误: ' . curl_error($tuCurl);
			}
			curl_close($tuCurl);
			return $tuData;
		}
```

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
