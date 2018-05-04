[TOC]

> [参考网址](http://anyproxy.io/cn/#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)

## 作为全局模块
### 安装
对于Debian或者Ubuntu系统，在安装AnyProxy之前，可能还需要安装 nodejs-legacy
`sudo apt-get install nodejs-legacy`
然后，安装AnyProxy
`npm install -g anyproxy`

### 启动
命令行启动AnyProxy，默认端口号8001
`anyproxy -i `  
-i 参数是解析https 网址

将终端(如手机)的wifi 中高级设计代理 主机名为 电脑端的` IPv4 地址 网址` 端口为`8001`

电脑端启动可视化web访问`http://127.0.0.1:8002`

## 代理HTTPS
AnyProxy默认不对https请求做处理，如需看到明文信息，需要配置CA证书
解析https请求的原理是中间人攻击（man-in-the-middle），用户必须信任AnyProxy生成的CA证书，才能进行后续流程

### 生成证书
`anyproxy-ca `
### 安装证书
在电脑和终端都安装证书
[查看各平台如何安装证书](http://anyproxy.io/cn/#%E8%AF%81%E4%B9%A6%E9%85%8D%E7%BD%AE)

### 启动
` anyproxy --i` 