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

### CRT - certificate
证书,常见于`*NIX系统  `
PEM 和DER 格式均有 ,多为PEM格式

### CER 
证书  ,常见于Windows系统,同样的,
PEM 和DER 格式均有 ,多为DER格式

###	KEY 
用来存放一个公钥或者私钥,
并非X.509证书,
PEM 和DER 格式均有
查看PEM 格式的 KEY的办法:`openssl rsa -in mykey.key -text -noout`
如果是DER格式的`openssl rsa -in mykey.key -text -noout -inform der`

### CSR
CSR - Certificate Signing Request,即证书签名请求,
这个不是证书,而是向权威证书颁发机构获得签名证书的申请,其核心内容是一个公钥(含其他信息),
在生成这个申请的时候,同时也会生成一个私钥,私钥要自己保管好
查看的办法:	`openssl req -noout -text -in my.csr` DER格式 加 `-inform der`)

### PFX/P12
PFX/P12 - predecessor of PKCS#12
对`*nix 服务器`来说,一般CRT和KEY是分开存放在不同文件中的
但Windows的IIS则将它们存在一个PFX文件中,PFX通常会有一个"提取密码"

PFX使用的时DER编码,何把PFX转换为PEM编码？
`openssl pkcs12 -in for-iis.pfx -out for-iis.pem -nodes`
这个时候会提示你输入提取代码. for-iis.pem就是可读的文本.
生成pfx的命令类似这样:
`openssl pkcs12 -export -in certificate.crt -inkey privateKey.key -out certificate.pfx -certfile CACert.crt`

其中CACert.crt是CA(权威证书颁发机构)的根证书,有的话也通过-certfile参数一起带进去.这么看来,PFX其实是个证书密钥库.

###  JKS
JKS - 即Java Key Storage,
这是Java的专利,跟OpenSSL关系不大,利用Java的一个叫"keytool"的工具,可以将PFX转为JKS,keytool也能直接生成JKS,

### 证书编码的转换
PEM转为DER 
`openssl x509 -in cert.crt -outform der -out cert.der`

DER转为PEM
`openssl x509 -in cert.crt -inform der -outform pem -out cert.pem`

替换的参数可根据生成时所用参数参考
要转换KEY文件把x509换成rsa,
要转CSR的话,把x509换成req
要转PFX/P12的话,把x509换成pkcs12


### 获得证书
### 向权威证书颁发机构申请证书

用这命令生成一个csr: 
`openssl req -newkey rsa:2048 -new -nodes -keyout my.key -out my.csr`
把csr交给权威证书颁发机构,权威证书颁发机构对此进行签名,完成.保留好csr,
当权威证书颁发机构颁发的证书过期的时候,你还可以用同样的csr来申请新的证书,key保持不变.

### 或者生成自签名的证书
`openssl req -newkey rsa:2048 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem`
在生成证书的过程中会要你填一堆的东西,其实真正要填的只有Common Name,通常填写你服务器的域名,如"demo.com",或者你服务器的IP地址,其它都可以留空的.

生产环境中还是不要使用自签的证书,否则浏览器会不认,或者如果你是企业应用的话能够强制让用户的浏览器接受你的自签证书也行.

向权威机构要证书通常是要钱的,但现在也有免费的,仅仅需要一个简单的域名验证即可.有兴趣的话查查"沃通数字证书".


