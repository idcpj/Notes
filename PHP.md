[TOC]

## 定时备份
如果 `php /data/www/demo/index.php  app sendApi cron`  无法备份,
可以使用访问地址的形式 `curl  http://www.demo.com/app/sendapi/cron`


## https双向认证

```php
function gethttpsdata($strurl){  
    $tuCurl = curl_init();   
    curl_setopt($tuCurl, CURLOPT_URL, $strurl);   
    curl_setopt($tuCurl, CURLOPT_PORT , 443);   
    curl_setopt($tuCurl, CURLOPT_VERBOSE, 0);   
    curl_setopt($tuCurl, CURLOPT_HEADER, 0);   
    curl_setopt($tuCurl, CURLOPT_SSLVERSION, 3);   
      
    curl_setopt($tuCurl, CURLOPT_SSLCERT,"/newcert.pem");   
    curl_setopt($tuCurl, CURLOPT_SSLCERTPASSWD,"xiaozl");  
    curl_setopt($tuCurl, CURLOPT_SSLCERTTYPE,"PEM");  
      
    curl_setopt($tuCurl, CURLOPT_SSLKEY, getcwd()."/newkey.pem");   
    curl_setopt($tuCurl, CURLOPT_SSLKEYPASSWD,"xiaozl");  
    curl_setopt($tuCurl, CURLOPT_SSLKEYTYPE,"PEM");   
      
    curl_setopt($tuCurl, CURLOPT_CAINFO,"/cacert.pem");   
       
    curl_setopt($tuCurl, CURLOPT_POST, 1);   
    curl_setopt($tuCurl, CURLOPT_SSL_VERIFYPEER, 1);   
    curl_setopt($tuCurl, CURLOPT_RETURNTRANSFER, 1);   
      
    //curl_setopt($tuCurl, CURLOPT_POSTFIELDS, $data);   
    //curl_setopt($tuCurl, CURLOPT_HTTPHEADER, array("Content-Type: text/xml","SOAPAction: \"/soap/action/query\"", "Content-length: ".strlen($data)));   
      
    $tuData = curl_exec($tuCurl);   
    if(!curl_errno($tuCurl)){   
      $info = curl_getinfo($tuCurl);   
     // echo 'Took ' . $info['total_time'] . ' seconds to send a request to ' . $info['url'];   
    } else {   
      echo 'Curl error: ' . curl_error($tuCurl);   
    }   
    curl_close($tuCurl);   
    echo $tuData;   
}  
```


