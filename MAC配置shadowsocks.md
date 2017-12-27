[TOC]


>参考网站  [macOS 安装 shadowsocks 及配置插件](http://lonf.me/2017/01/06/macOS-shadowsocks-Proxy-SwitchyOmega/#%E9%85%8D%E7%BD%AE-shadowsocks)
>参考网站 [ShadowsocksX-NG](https://github.com/shadowsocks/ShadowsocksX-NG/releases) 下载影梭

*如果要安装命令版的 查看参看文档*

## 安装 Proxy SwitchyOmega
安装google 商店[Proxy SwitchyOmega](https://chrome.google.com/webstore/detail/proxy-switchyomega/padekgcemlokbadohgkifijomclgjgif)

在连接 shadowsocks 打开的情况下 Chrome
` open -a "/Applications/Google Chrome.app" --args --proxy-server="socks5://127.0.0.1:1080"`



## 配置 Proxy SwitchyOmega
下载备份好的配置文件:

https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList.bak


导入配置文件：
`设定 –> 导入/导出 –> 从配置文件恢复 –> 选择刚刚下载好的配置文件(会生成新的情景模式GWFed)`

添加代理服务器：
` 情景模式 –> GFWed –> 代理服务器 –> 代理协议 socks5 –> 代理服务器 127.0.0.1 –> 代理端口 1080`

