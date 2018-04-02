[TOC]

> [参考网站](http://www.cnblogs.com/guogangj/p/4118605.html)
> [HTTPS证书转换成PEM格式](https://help.aliyun.com/knowledge_detail/40526.html)

## SSL 与OpenSSL 区别
SSL 是一个加密算法,属于理论,OpenSSL 是这个算法的一个实现

## 证书标准
X.509 - 这是一种证书标准,有两中编码格式

## 编码格式

### PEM

PEM ( Privacy Enhanced Mail ) ,打开看文本格式,
以"-----BEGIN..."开头, "-----END..."结尾,
内容是BASE64编码.
查看PEM格式证书的信息:
`openssl x509 -in certificate.pem -text -noout`
Apache和*NIX服务器偏向于使用这种编码格式.

### DER

DER ( Distinguished Encoding Rules ) 
内容是二进制编码,
查看DER格式证书的信息:
`openssl x509 -in certificate.der -inform der -text -noout`
Java和Windows服务器偏向于使用这种编码格式.

## 相关的文件扩展名
虽然有PEM和DER这两种编码格式,但文件扩展名并不一定就叫"PEM"或者"DER"

### 