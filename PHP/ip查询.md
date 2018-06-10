[TOC]

> 网址 [ipip.net](https://www.ipip.net/)


1. 通过线上免费查询(每天1000次)
接口:
```
http://freeapi.ipip.net/112.12.8.8 
返回 json
`
[
"中国",
"浙江",
"金华",
"",
"移动"
]
```

2. 下载离线库
[网址](https://www.ipip.net/product/ip.html)
含有封装好的类
```
$rep = Ip::find($ip);

``

3. 更多付费查询
[网址](https://www.ipip.net/api.html)