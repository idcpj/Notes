[TOC]

> [官网下载](https://www.wireshark.org/download.html)

## 使用
### 快速生成过滤
在需要过滤列表字段右键
![](images/Snipaste_2018-10-30_11-44-34.png)

## 过滤规则
### 对 ip 端口 和http 进行过滤
`(ip.src == 192.168.0.91) && (tcp.srcport == 8000) and http`

